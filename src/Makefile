APP = Spin
MFILES = 
matlabversion = 2018b
DELETE_FILES =
BIN = ../bin
#RP_DIR = $(shell . /etc/environ.sh; use -e -r rappture; echo $${RAPPTURE_PATH})

MCCFLAGS = -v -C -m
#MCCINCLUDES = -I $(RP_DIR)/lib/matlab

$(APP): $(APP).m $(MFILES)
	#mcc $(MCCFLAGS) $(MCCINCLUDES) $(APP).m $(MFILES)
	mcc $(MCCFLAGS) $(APP).m $(MFILES)
	#patchrunscript.sh run_$(APP).sh run_$(APP).sh

all:
	. /etc/environ.sh; use -e -r matlab-$(matlabversion); make $(APP)

install: all
	install --mode 0755 -D run_$(APP).sh $(BIN)
	install --mode 0755 -D $(APP) $(BIN)
	#install --mode 0644 -D readme.txt $(BIN)/$(APP).readme
	if [ -e $(APP).ctf ] ; then \
        mv $(APP).ctf $(BIN); \
        cd $(BIN); \
        . /etc/environ.sh; \
        use -e -r matlab-$(matlabversion); \
        extractCTF $(APP).ctf; \
    fi

clean:
	rm -f $(APP) $(APP).ctf \
         $(APP).prj run_$(APP).sh \
         $(APP)_main.c $(APP)_mcc_component_data.c \
         mccExcludedFiles.log $(DELETE_FILES)

distclean: clean
	rm -rf $(BIN)/$(APP) \
          $(BIN)/$(APP).ctf \
          $(BIN)/$(APP)_mcr \
          $(BIN)/run_$(APP).sh

