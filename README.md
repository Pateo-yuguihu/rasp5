# rasp5
rasp5 project

git push -u -f origin main


#AT24C256 write/read

Use i2c-utils to read and write

# write to 0x0000. First 0x00 is the register offset, second 0x00 is the first byte of DATA,
# but chip interprets that as the 2nd byte of the address.
# 16bit 寄存器地址写入数据
i2cset -y 1 0x6c 0x00 0x00 0x01 0x02 0x03 i
i2cset -y 1 0x6c 0x00 0x0a 0xFF 0xFE 0xFD i

# 设置地址
# write address 0x0000 to the chip, sets the address counter
i2cset -y 1 0x6c 0x00 0x00

#开始读
# each read command returns a byte and advances the counter
ic2get -y 1 0x6c # returns 0x01
ic2get -y 1 0x6c # returns 0x02
ic2get -y 1 0x6c # returns 0x03

# repeat the process to read address 0x000A
i2cset -y 1 0x6c 0x00 0x0a
ic2get -y 1 0x6c # returns 0xFF
ic2get -y 1 0x6c # returns 0xFE
ic2get -y 1 0x6c # returns 0xFD
