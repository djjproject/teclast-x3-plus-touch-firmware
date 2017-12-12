# Teclast X3 Plus Linux / Android touch Firmware

## Reference file
https://github.com/onitake/gsl-firmware/

## Generation Method

- SileadTouch.sys -> firmware.fw

	<code>export F=/root/gsl-firmware/teclast/SileadTouch.sys</code>
    <pre><code>cat $F | hexdump -e '1/1  "0x%8.8_ax"' -e '1/1"%8._ad"' -e '8/1 "%02X ""\n"""' | grep -i -E "F0 00 00 00 02 00 00 00|7C 00 00 00 .. .. .. .." | grep "F0 00 00 00 02 00 00 00" -B1; echo --; cat $F | hexdump -e '1/1  "0x%8.8_ax    "' -e '1/1  "%8._ad    "' -e '8/1 "%02X ""\n"""' | grep -i -E "F0 00 00 00 02 00 00 00|7C 00 00 00 .. .. .. .." | tail -n2</code></pre>
    
    <code>dd bs=1 if=$F of=firmware.fw skip=57952  count=$(( 99392 -  57952 + 8))</code>

- firmware.fw -> silead_ts.fw

	<code>./fwtool -c firmware.fw -m 1680 -w 1980 -h 1500 -t 10 -f track silead_ts.fw</code>

## Using Video
https://www.youtube.com/watch?v=aeT23rZcuoc

## Installation Method
in android terminnal. just type below.

<code>cd /lib/firmware</code>

<code>rm silead_ts.fw</code>

<code>mv /sdcard/Download/silead_tw.fw .</code>

<code>chmod 755 silead_ts.fw</code>
