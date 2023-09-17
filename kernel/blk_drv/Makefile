#
# Makefile for the FREAX-kernel block device drivers.
#
# Note! Dependencies are done automagically by 'make dep', which also
# removes any old dependencies. DON'T put your own dependencies here
# unless it's something special (ie not a .c file).
#
# ע�⣡������ϵ����'make dep'�Զ����еģ���Ҳ���Զ�ȥ��ԭ����������Ϣ����Ҫ�����Լ���
# ������ϵ��Ϣ��������������ر��ļ��ģ�Ҳ������һ��.c �ļ�����Ϣ����
# (Linux ��������ֽ�FREAX��������ftp.funet.fi �Ĺ���Ա�ĳ�Linux �������)��

AR =gar # GNU �Ķ������ļ������������ڴ������޸��Լ��ӹ鵵�ļ��г�ȡ�ļ���
AS =gas # GNU �Ļ�����
LD =gld # GNU �����ӳ���
LDFLAGS =-s -x # ���ӳ������еĲ�����-s ����ļ���ʡ�����з�����Ϣ��-x ɾ�����оֲ����š�
CC =gcc # GNU C ���Ա�������
# ��һ����C �������ѡ�-Wall ��ʾ���еľ�����Ϣ��-O �Ż�ѡ��Ż����볤�Ⱥ�ִ��ʱ�䣻
# -fstrength-reduce �Ż�ѭ��ִ�д��룬�ų��ظ�������-fomit-frame-pointer ʡ�Ա��治��Ҫ
# �Ŀ��ָ�룻-fcombine-regs �ϲ��Ĵ��������ټĴ������ʹ�ã�-finline-functions �����м�
# ����С�ĺ�������Ƕ����ó����У�-mstring-insns Linus �Լ���ӵ��Ż�ѡ��Ժ���ʹ�ã�
# -nostdinc -I../include ��ʹ��Ĭ��·���еİ����ļ�����ʹ��ָ��Ŀ¼�е�(../../include)��
CFLAGS =-Wall -O -fstrength-reduce -fomit-frame-pointer -fcombine-regs \
-finline-functions -mstring-insns -nostdinc -I../../include
# C ǰ����ѡ�-E ֻ����C ǰ������������ָ����C �������Ԥ����������������������׼��
# ���豸��ָ��������ļ��У�-nostdinc -I../../include ͬǰ��
CPP =gcc -E -nostdinc -I../../include

# ����Ĺ���ָʾmake ���������������е�.c �ļ���������.s �����򡣸ù��������
# ָʹgcc ����CFLAGS ��ָ����ѡ���C �������󲻽��л���ֹͣ��-S�����Ӷ�������
# ����ĸ���C �ļ���Ӧ�Ļ������ļ���Ĭ��������������Ļ������ļ�����ԭC �ļ���
# ȥ��.c ������.s ��׺��-o ��ʾ���������ļ������ơ�����$*.s����$@�����Զ�Ŀ�������
# $<������һ���Ⱦ����������Ｔ�Ƿ�������*.c ���ļ���
.c.s:
$(CC) $(CFLAGS) \
-S -o $*.s $<
# ��������ʾ������.s �������ļ������.o Ŀ���ļ���22 ����ʵ�ָò����ľ������
.s.o:
$(AS) -c -o $*.o $<
.c.o: # �������棬*.c �ļ�-??*.o Ŀ���ļ������������ӡ�
$(CC) $(CFLAGS) \
-c -o $*.o $<

OBJS = ll_rw_blk.o floppy.o hd.o ramdisk.o # ����Ŀ���ļ�����OBJS��

# �������Ⱦ�����OBJS ��ʹ��������������ӳ�Ŀ��blk_drv.a ���ļ���
blk_drv.a: $(OBJS)
$(AR) rcs blk_drv.a $(OBJS)
sync

# ����Ĺ�������������������ִ��'make clean'ʱ���ͻ�ִ��34--35 ���ϵ����ȥ�����б���
# �������ɵ��ļ���'rm'���ļ�ɾ�����ѡ��-f �����Ǻ��Բ����ڵ��ļ������Ҳ���ʾɾ����Ϣ��
clean:
rm -f core *.o *.a tmp_make
for i in *.c;do rm -f `basename $$i .c`.s;done

# �����Ŀ���������ڼ����ļ�֮���������ϵ���������£�
# ʹ���ַ����༭����sed ��Makefile �ļ������Ǳ��ļ������д��������Ϊɾ��Makefile
# �ļ���'### Dependencies'�к���������У������44 ��ʼ���У���������tmp_make
# ��ʱ�ļ���38 �е����ã���Ȼ���kernel/blk_drv/Ŀ¼�µ�ÿ��C �ļ�ִ��gcc Ԥ��������.
# -M ��־����Ԥ���������������ÿ��Ŀ���ļ�����ԵĹ��򣬲�����Щ�������make �﷨��
# ����ÿһ��Դ�ļ���Ԥ�����������һ��make ����������ʽ����ӦԴ�����ļ���Ŀ��
# �ļ���������������ϵ--��Դ�ļ��а���������ͷ�ļ��б�����Ԥ������������ӵ���ʱ
# �ļ�tmp_make �У�Ȼ�󽫸���ʱ�ļ����Ƴ��µ�Makefile �ļ���
dep:
sed '/\#\#\# Dependencies/q' < Makefile > tmp_make
(for i in *.c;do echo -n `echo $$i | sed 's,\.c,\.s,'`" "; \
$(CPP) -M $$i;done) >> tmp_make
cp tmp_make Makefile

### Dependencies:
floppy.s floppy.o : floppy.c ../../include/linux/sched.h ../../include/linux/head.h \
../../include/linux/fs.h ../../include/sys/types.h ../../include/linux/mm.h \
../../include/signal.h ../../include/linux/kernel.h \
../../include/linux/fdreg.h ../../include/asm/system.h \
../../include/asm/io.h ../../include/asm/segment.h blk.h
hd.s hd.o : hd.c ../../include/linux/config.h ../../include/linux/sched.h \
../../include/linux/head.h ../../include/linux/fs.h \
../../include/sys/types.h ../../include/linux/mm.h ../../include/signal.h \
../../include/linux/kernel.h ../../include/linux/hdreg.h \
../../include/asm/system.h ../../include/asm/io.h \
../../include/asm/segment.h blk.h
ll_rw_blk.s ll_rw_blk.o : ll_rw_blk.c ../../include/errno.h ../../include/linux/sched.h \
../../include/linux/head.h ../../include/linux/fs.h \
../../include/sys/types.h ../../include/linux/mm.h ../../include/signal.h \
../../include/linux/kernel.h ../../include/asm/system.h blk.h