#
# SmallPlayer unit tests
# Build from SmallPlayer: make -f Tests/GNUmakefile
# Run: ./Tests/obj/test_SmallPlayer
#

include $(GNUSTEP_MAKEFILES)/common.make

SMALLSTEP_FRAMEWORK := $(shell find ../../SmallStepLib -name "SmallStep.framework" -type d 2>/dev/null | head -1)
ifneq ($(SMALLSTEP_FRAMEWORK),)
  SMALLSTEP_LIB_DIR := $(shell cd $(SMALLSTEP_FRAMEWORK)/Versions/0 2>/dev/null && pwd)
  SMALLSTEP_LIB_PATH := -L$(SMALLSTEP_LIB_DIR)
  SMALLSTEP_LDFLAGS := -Wl,-rpath,$(SMALLSTEP_LIB_DIR)
else
  SMALLSTEP_LIB_PATH := -L../../SmallStepLib/obj
  SMALLSTEP_LDFLAGS :=
endif

FFMPEG_CFLAGS := $(shell pkg-config --cflags libavformat libavcodec libavutil libswscale 2>/dev/null)
FFMPEG_LIBS   := $(shell pkg-config --libs libavformat libavcodec libavutil libswscale 2>/dev/null)

TOOL_NAME = test_SmallPlayer
test_SmallPlayer_OBJC_FILES = SmallPlayerTests.m ../Sources/App/AppDelegate.m ../Sources/Player/SPPlayerEngine.m ../Sources/Player/SPPlayerView.m ../Sources/Backend/SPPlayerBackend.m ../Sources/Backend/SPFFmpegPlayerBackend.m ../Sources/Backend/SPMplayerBackend.m ../Sources/Backend/SPMencoderBackend.m ../Sources/Backend/SPMpvBackend.m
test_SmallPlayer_C_FILES = ../Sources/Backend/SPFFmpegBackend.c
test_SmallPlayer_INCLUDE_DIRS = -I.. -I../Sources/App -I../Sources/Player -I../Sources/Backend
test_SmallPlayer_INCLUDE_DIRS += -I../../SmallStepLib/SmallStep/Core -I../../SmallStepLib/SmallStep/Platform/Linux -I../../SmallStepLib/Tests
test_SmallPlayer_INCLUDE_DIRS += $(FFMPEG_CFLAGS)
test_SmallPlayer_TOOL_LIBS = -lSmallStep -lgnustep-gui -lgnustep-base -lobjc $(FFMPEG_LIBS)
test_SmallPlayer_LDFLAGS = $(SMALLSTEP_LIB_PATH) $(SMALLSTEP_LDFLAGS) -Wl,--allow-shlib-undefined

before-all::
	$(MAKE) -C ../../SmallStepLib
	$(MAKE) -C ..

include $(GNUSTEP_MAKEFILES)/tool.make
