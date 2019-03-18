
vpath %.cpp src
vpath %.hpp include

.SUFFIXES:
.SUFFIXES: .cpp .hpp

SHELL         = /bin/sh

COMPILERWARN  = 
OPTIMIZATIONS = -falias -fast -m64 -mtune=core-avx2 -fstrict-aliasing -funroll-loops
BUILDFLAGS    =    $(COMPILERWARN) $(OPTIMIZATIONS)

CC            =  icc
CXX           =  icpc
CFLAGS        = -std=c11   $(OPTIMIZATIONS)
CXXFLAGS      = -std=c++17 $(OPTIMIZATIONS)

SOURCES_DIR   = src
INCLUDES_DIR  = include

MKLINCLUDES   = -I $(MKLINCLUDEDIR)
IPPINCLUDES   = -I $(INTELIPPINCLUDEDIR)
IPPCPINCLUDES = -I $(INTELIPPCPINCLUDEDIR)
INTELINCLUDES =    $(INTELIPPINCLUDES) $(INTELIPPCPINCLUDES)
SRC_HEADERS   = -I $(INCLUDES_DIR)
INCLUDEDIRS   =    $(SRC_HEADERS) $(INTELINCLUDES)

BOOST_OPTS    = -lboost_program_options
BOOST_LIBS    =    $(BOOST_OPTS)
MKLLIB        = -L $(MKLLIBDIR)        -lmkl
IPPLIB        = -L $(INTELIPPLIBDIR)   -lippcc -lippcore
IPPCPLIB      = -L $(INTELIPPCPLIBDIR) -lippcp
INTEL_LIBS    =    $(IPPLIB) $(IPPCPLIB)
REQLIBS       =    $(BOOST_LIBS) $(INTEL_LIBS)

SRCS          = main.cpp
OBJS          = $(patsubst %.cpp, %.o, $(SRCS))
PROGRAM       = fbp

OUTPUT_OPTION = -o $@
TARGET_ARCH   = 

COMPILE.cpp   = $(CXX) $(CXXFLAGS) $(CPPFLAGS) $(INCLUDEDIRS) $(TARGET_ARCH) -c
LINK.o        = $(CXX) $(CXXFLAGS) $(CPPFLAGS) $(INCLUDEDIRS) $(TARGET_ARCH) $(LDFLAGS) 

all: $(PROGRAM)

$(PROGRAM): $(OBJS)
	$(LINK.o) $(OUTPUT_OPTION) $^ $(REQLIBS)

%.o: %.cpp 
	$(COMPILE.cpp) $(OUTPUT_OPTION) $^ 

.PHONY: clean
clean:
	$(RM) $(OBJS) $(PROGRAM)
