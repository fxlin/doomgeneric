################################################################
#
# $Id:$
#
# $Log:$
#		xzl: based on -sdl makefile

ifeq ($(V),1)
	VB=''
else
	VB=@
endif


#SDL_CFLAGS = `sdl2-config --cflags`
#SDL_LIBS = `sdl2-config --cflags --libs` -lSDL2_mixer

CC=aarch64-linux-gnu-gcc-9
CFLAGS+=-ggdb3 -O0    # -Os (now has some bug with this  .. page permission
CFLAGS+=-Wall -DNORMALUNIX -DLINUX -DSNDSERV -D_DEFAULT_SOURCE # -DUSEASM
#CFLAGS+=-DFEATURE_SOUND $(SDL_CFLAGS)

# xzl: own newlib
CFLAGS += -nostdlib -nostdinc -nostartfiles -ffreestanding
CFLAGS += -I /home/xzl/p1-kernel-next-wsl2/src/current/usr/newlib/newlib/libc/include
CFLAGS += -I /home/xzl/p1-kernel-next-wsl2/src/current/usr/libminisdl/include/

# libgcc (e.g. stddef.h
CFLAGS += -I /usr/lib/gcc-cross/aarch64-linux-gnu/9/include/

LDFLAGS += -Wl,--gc-sections
LDFLAGS += -static -T user.ld -nostdlib -nostartfiles -ffreestanding -static

LIBS+=/home/xzl/p1-kernel-next-wsl2/src/current/usr/libminisdl/libminisdl.a
LIBS+=/home/xzl/p1-kernel-next-wsl2/src/current/usr/libnew.a
LIBS+=-lm -lc
LIBS+=-lgcc 

LDFLAGS += -L /home/xzl/p1-kernel-next-wsl2/src/current/usr/newlib/build-aarch64

# subdirectory for objects
OBJDIR=build
OUTPUT=doomgeneric

SRC_DOOM = dummy.o am_map.o doomdef.o doomstat.o dstrings.o d_event.o d_items.o d_iwad.o d_loop.o d_main.o d_mode.o d_net.o f_finale.o f_wipe.o g_game.o hu_lib.o hu_stuff.o info.o i_cdmus.o i_endoom.o i_joystick.o i_scale.o i_sound.o i_system.o i_timer.o memio.o m_argv.o m_bbox.o m_cheat.o m_config.o m_controls.o m_fixed.o m_menu.o m_misc.o m_random.o p_ceilng.o p_doors.o p_enemy.o p_floor.o p_inter.o p_lights.o p_map.o p_maputl.o p_mobj.o p_plats.o p_pspr.o p_saveg.o p_setup.o p_sight.o p_spec.o p_switch.o p_telept.o p_tick.o p_user.o r_bsp.o r_data.o r_draw.o r_main.o r_plane.o r_segs.o r_sky.o r_things.o sha1.o sounds.o statdump.o st_lib.o st_stuff.o s_sound.o tables.o v_video.o wi_stuff.o w_checksum.o w_file.o w_main.o w_wad.o z_zone.o w_file_stdc.o i_input.o i_video.o doomgeneric.o 
SRC_DOOM += doomgeneric_minisdl.o
# SRC_DOOM += doomgeneric_sdl.o mus2mid.o i_sdlmusic.o i_sdlsound.o

OBJS += $(addprefix $(OBJDIR)/, $(SRC_DOOM))

all:	 $(OUTPUT)

clean:
	rm -rf $(OBJDIR)
	rm -f $(OUTPUT)
	rm -f $(OUTPUT).gdb
	rm -f $(OUTPUT).map

$(OUTPUT):	$(OBJS)
	@echo [Linking $@]
	$(VB)$(CC) $(CFLAGS) $(LDFLAGS) $(OBJS) \
	-o $(OUTPUT) $(LIBS)

$(OBJS): | $(OBJDIR)

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(OBJDIR)/%.o:	%.c
	@echo [Compiling $<]
	$(VB)$(CC) $(CFLAGS) -c $< -o $@

print:
	@echo OBJS: $(OBJS)

