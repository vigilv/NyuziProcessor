#
# Copyright 2011-2015 Jeff Bush
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

TOPDIR=../../..

include $(TOPDIR)/build/target.mk

SRCS=initdata.c start.s

OBJS=$(SRCS_TO_OBJS)
DEPS=$(SRCS_TO_DEPS)

program.elf: $(OBJS)
	$(LD) -o program.elf -Ttext=0x1000 $(OBJS)

#
# To run, this uses the kernel built in software/kernel.
# The compiled initdata program is bundled into the filesystem
# and loaded by the kernel.
#
run: program.elf fsimage.bin
	$(EMULATOR) -b fsimage.bin $(TOPDIR)/software/kernel/kernel.hex

verirun: program.elf fsimage.bin
	$(VERILATOR) +bin=$(TOPDIR)/software/kernel/kernel.hex +block=fsimage.bin

fsimage.bin: program.elf
	$(MKFS) fsimage.bin program.elf

clean:
	rm -f program.elf fsimage.bin

-include $(DEPS)
