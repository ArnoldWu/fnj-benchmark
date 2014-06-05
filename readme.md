<h1>LyveMinds Firmware Benchmark Utilities</h1>
This repository contains open source utilities used by the LyveMinds firmware group to characterize new hardware platforms.
 
<h2>Utilities</h2>
bonnie - File system IO performance<br />
glmark2 - OpenGL ES 2.0 benchmark<br />
iperf - Network io performance<br />
shatest - OpenSSL SHA256 test program<br />
<br />
<table class="confluenceTable"><tbody><tr><th class="confluenceTh">Component</th><th class="confluenceTh">Tool</th><th colspan="1" class="confluenceTh">Example</th></tr><tr><td class="confluenceTd">Ethernet</td><td class="confluenceTd">iperf</td><td colspan="1" class="confluenceTd"><p>Host: <br /> iperf -s -p 9002 <br />Client:<br /> iperf -c 192.168.1.66 -p 9002 -t 20 -P 1</p><p><span> iperf -c 192.168.1.66 -p 9002 -t 20 -P 5</span></p></td></tr><tr><td class="confluenceTd">Wifi</td><td class="confluenceTd"><p>iperf</p><p> </p></td><td colspan="1" class="confluenceTd"><p>Host: <br /> iperf -s -p 9002 <br />Client:<br /> iperf -c 192.168.1.66 -p 9002 -t 20 -P 1</p><p>iperf -c 192.168.1.66 -p 9002 -t 20 -P 5</p></td></tr><tr><td class="confluenceTd">eMMC</td><td class="confluenceTd"><p>bonnie</p></td><td colspan="1" class="confluenceTd"><p>cd to eMMC directory</p><p>bonnie -d testdir -u 0:0</p></td></tr><tr><td class="confluenceTd"><p>SATA</p></td><td class="confluenceTd"><p>bonnie</p></td><td colspan="1" class="confluenceTd"><p>cd to SATA directory</p><p><span> bonnie<span> -d testdir -u 0:0</span></span></p></td></tr><tr><td class="confluenceTd">USB</td><td class="confluenceTd"><span>bonnie</span></td><td class="confluenceTd"><p>mount USB mass storage device</p><p><span>cd to USB drive directory</span></p><p><span><span> bonnie</span><span> -d testdir -u 0:0</span></span></p></td></tr><tr><td colspan="1" class="confluenceTd">GPU</td><td colspan="1" class="confluenceTd"><a href="/wiki/download/attachments/39223354/Glmark2Activity-debug.apk?version=1&amp;modificationDate=1400116012537&amp;api=v2">glmark2</a></td><td colspan="1" class="confluenceTd"><p>am start -a android.intent.action.MAIN -n org.linaro.glmark2/org.linaro.glmark2.Glmark2Activity</p><p>logcat | grep FPS</p></td></tr><tr><td colspan="1" class="confluenceTd">CPU</td><td colspan="1" class="confluenceTd"><p>shatest</p><p><span>JPEG decode</span></p></td><td colspan="1" class="confluenceTd"><p>shatest &lt;filename&gt;</p><p><span>TODO - Adding to glmark2 tests</span></p></td></tr></tbody></table></div><h3 id="NewHardwareEvaluation-EthernetandWifi">Ethernet and Wifi</h3><p>iperf is a simple and easy way to test single and multiple stream connections through Ethernet or WiFi.  Two baseline tests with 1 stream and 5 simultaneous stream seem the most useful are.</p><p style="margin-left: 30.0px;">Host:  </p><p style="margin-left: 60.0px;">iperf -s -p 9002  </p><p style="margin-left: 30.0px;">Client:</p><p style="margin-left: 60.0px;">iperf -c &lt;ip address&gt; -p 9002 -t 20 -P &lt;#streams&gt;*</p><p style="margin-left: 30.0px;">* Testing with 1 stream and 5 TCP streams seems sufficient for characterizing throughput for an interface.</p><p>See <a href="https://blackpearlsystems.atlassian.net/wiki/display/FE/Network+Performance+Characterization" style="line-height: 1.4285715;" rel="nofollow">Network Performance Characterization</a> for more details on iperf tests done on the HDC.</p><h3 id="NewHardwareEvaluation-eMMC,SATAandUSBDiskIO">eMMC, SATA and USB Disk IO</h3><p>A quick IO performance test using DD results in the following read/write performance.</p><p style="margin-left: 30.0px;">Write:  </p><p style="margin-left: 60.0px;">dd bs=4096 count=4096 if=/dev/zero of=test conv=fdatasync</p><p style="margin-left: 30.0px;">Read:  </p><p style="margin-left: 60.0px;">dd bs=4096 count=4096 if=test of=/dev/null conv=fdatasync</p><div>We have also been using <a href="/wiki/download/attachments/39223354/Androbench%20%28Storage%20Benchmark%29.apk?version=1&amp;modificationDate=1400116124048&amp;api=v2">AndrodBench</a> to get random access statistics for a device. See <a href="https://blackpearlsystems.atlassian.net/wiki/display/FE/Import+Profiling" rel="nofollow">Import Profiling HDC IO Tests</a> for an example.</div><h3 id="NewHardwareEvaluation-GPU">GPU</h3><div><div><p>A test program called <a href="/wiki/download/attachments/39223354/LyveProf.apk?version=1&amp;modificationDate=1400116089761&amp;api=v2">LyveProf</a> was used to produce frame rate statistics rending exactly like the HDC currently does. </p><div class="table-wrap"><table class="confluenceTable"><tbody style="margin-left: 30.0px;"><tr style="margin-left: 30.0px;"><td class="confluenceTd"> </td><td style="margin-left: 90.0px;" class="confluenceTd">Dual Lite</td><td style="margin-left: 90.0px;" class="confluenceTd">Dual Lite w/HDMI</td><td style="margin-left: 90.0px;" class="confluenceTd">Quad</td><td style="margin-left: 90.0px;" class="confluenceTd">Quad w/HDMI</td><td style="margin-left: 90.0px;" class="confluenceTd">A10*</td></tr><tr style="margin-left: 90.0px;"><td style="margin-left: 90.0px;" class="confluenceTd">Slideshow:</td><td style="margin-left: 90.0px;" class="confluenceTd">60</td><td style="margin-left: 90.0px;" class="confluenceTd">26</td><td style="margin-left: 90.0px;" class="confluenceTd">60</td><td style="margin-left: 90.0px;" class="confluenceTd">36</td><td style="margin-left: 90.0px;" class="confluenceTd">50</td></tr><tr style="margin-left: 90.0px;"><td style="margin-left: 90.0px;" class="confluenceTd">Slideshow w/Blur:</td><td style="margin-left: 90.0px;" class="confluenceTd">12</td><td style="margin-left: 90.0px;" class="confluenceTd">3</td><td style="margin-left: 90.0px;" class="confluenceTd">19</td><td style="margin-left: 90.0px;" class="confluenceTd">5</td><td style="margin-left: 90.0px;" class="confluenceTd">4</td></tr><tr style="margin-left: 90.0px;"><td style="margin-left: 90.0px;" class="confluenceTd">Fling:</td><td style="margin-left: 90.0px;" class="confluenceTd">59</td><td style="margin-left: 90.0px;" class="confluenceTd">21</td><td style="margin-left: 90.0px;" class="confluenceTd">59</td><td style="margin-left: 90.0px;" class="confluenceTd">22</td><td style="margin-left: 90.0px;" class="confluenceTd">46</td></tr><tr style="margin-left: 90.0px;"><td style="margin-left: 90.0px;" class="confluenceTd">Fling w/Blur:</td><td style="margin-left: 90.0px;" class="confluenceTd">12</td><td style="margin-left: 90.0px;" class="confluenceTd">3</td><td style="margin-left: 90.0px;" class="confluenceTd">19</td><td style="margin-left: 90.0px;" class="confluenceTd">4</td><td style="margin-left: 90.0px;" class="confluenceTd">4</td></tr></tbody></table>
