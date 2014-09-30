#
# Makefile for bbftp
#

STDOBJS = bbftp.o\
		bbftp_cd.o\
		bbftp_get.o\
		bbftp_lcd.o\
		bbftp_list.o\
		bbftp_mget.o\
		bbftp_mkdir.o\
		bbftp_mput.o\
		bbftp_put.o\
		bbftp_rm.o\
		bbftp_stat.o\
		bbftp_statfs.o\
		bbftp_dir.o\
		bbftp_retr.o\
		bbftp_setremotecos.o\
		bbftp_setremoteumask.o\
		bbftp_store.o\
		bbftp_socket.o\
		bbftp_utils.o\
		connecttoserver.o\
		getdatasock.o\
		readmessage.o\
		sendproto.o\
		treatcommand.o\
		bbftp_turl.o\
		writemessage.o\
		setsignals.o

OBJS = $(STDOBJS)   

STATUS_OBJS = bbftpstatus.o writemessage.o readmessage.o
#
# Headers
#
HEAD = ./bbftp.h \
        ../includes/bbftp_private.h\
        ../includes/bbftp_private_user.h\
		../includes/client.h\
		../includes/client_proto.h\
		../includes/common.h \
		../includes/config.h \
		../includes/daemon.h \
		../includes/status.h \
		../includes/structures.h\
		../includes/version.h 
#
# Main program
#
PROG = bbftp
STATUS_PROG = bbftpstatus
CC = cc
#
# Compiler and flags
#

# CPPFLAGS is ignored on ccdvrs01
CFLAGS = -g -O2 -DDARWIN -I../includes -I./ 
#CFLAGS = -g -O2 -DDARWIN
#CPPFLAGS = -I../includes -I./ 
#

LDFLAGS = 
LIBS =  -lcrypto -lz
GFWLIB = 
prefix = /usr/local
exec_prefix = ${prefix}
bindir = ${exec_prefix}/bin
mandir = ${prefix}/man

all: ${PROG} bbftpstatus

${OBJS} : ${HEAD}
${STATUS_OBJS} : ${HEAD}

../gfw/libgfw.a:
	(cd ../gfw; make clean; make)

${PROG} :${OBJS} ${GFWLIB}
	${CC} -o $@ ${OBJS} ${LDFLAGS} ${GFWLIB} ${LIBS} 

${STATUS_PROG} :${STATUS_OBJS}
	${CC} -o $@ ${STATUS_OBJS} ${LDFLAGS} ${LIBS} 

clean:
	rm -f ${OBJS}
	rm -rf obj.i686-apple-darwin11.2.0
	rm -f config.cache
	(cd ../gfw; make clean)
    
install:${PROG} ${STATUS_PROG}
	mkdir -p ${prefix}
	mkdir -p ${bindir}
	/usr/bin/install -c ${PROG} ${bindir}/${PROG}
	/usr/bin/install -c ${STATUS_PROG} ${bindir}/${STATUS_PROG}

install-doc:
	mkdir -p ${mandir}
	mkdir -p ${mandir}/man1
	/usr/bin/install -c ../doc/${PROG}.1 ${mandir}/man1/${PROG}.1

runtest: ${PROG}
	./${PROG} -v

doc-source: Doxyfile
	(cd ..;doxygen bbftpc/Doxyfile)
