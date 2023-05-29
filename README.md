# M480BSP_USB_HID_custom
 M480BSP_USB_HID_custom


update @ 2023/05/29

1. base on BSP USBD_HID_Transfer sample code ,  modify MCU and PC host tool

- PC host will issue CMD_SYNC to MCU , and start communication (INTERRUPT OUT)

- after MCU receive command , will reply modified data into commnad packet (INTERRUPT IN)

2. command packet : length : 58

- [HEAD] + [CODE] + [LEN] + [DATA..] + [CRC8] + [TAIL]

3. Below is MCU terminal log message

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/log_enable_USB_DEBUG_LOG.jpg)	

log message when execute windows tool 

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/windows_tool_log.jpg)	

command handsaking 

PC to MCU : CMD_SYNC ( 0x7F) , after MCU recieve and decode data , will plus 1 into data array then send to PC

PC to MCU : CMD_FUNC_01 ( 0x80) , after MCU recieve and decode data , will plus 0x10 into data array then send to PC

PC to MCU : CMD_FUNC_02 ( 0x81) , after MCU recieve and decode data , will plus 0x10 into data array then send to PC

PC to MCU : CMD_FUNC_03 ( 0x82) , after MCU recieve and decode data , will plus 0x10 into data array then send to PC

PC to MCU : CMD_FUNC_04 ( 0x83) , after MCU recieve and decode data , will plus 0x10 into data array then send to PC

PC to MCU : CMD_FUNC_05 ( 0x84) , after MCU recieve and decode data , will plus 0x10 into data array then send to PC

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/compare.jpg)	

4. below is USB capture tool log , 

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/USB_LA.jpg)	


5. under MCU code : hid_cmd.h , with define : USB_DEBUG_LOG

under Windows tool code : hid_cmd.h , with define : USB_DEBUG_LOG , USB_DELAY

if remove USB_DEBUG_LOG , below is USB capture tool log and time stamp

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/USB_LA_remove_printf.jpg)	

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/USB_LA_remove_printf_IN_OUT_timestamp.jpg)	


if remove USB_DELAY , below is USB capture tool log and time stamp

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/USB_LA_remove_delay.jpg)	

![image](https://github.com/released/M480BSP_USB_HID_custom/blob/main/USB_LA_remove_delay_IN_OUT_timestamp.jpg)	

