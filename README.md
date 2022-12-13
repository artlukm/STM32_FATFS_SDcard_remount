# STM32_FATFS_SDcard_remount

How to proper remount SD card using FATFS.
STM32 and SD card FATFS via SPI.

If your code works fine, but after reinstalling the SD card, it no longer works, most likely you are facing the this problem.
When reinserting the card. Function f_mount() no longer works, returns an error FR_DISK_ERR.
to solve the problem, you need to add the function of zeroing the structure field in diskio.c.

void disk_DeInitialize (
	BYTE pdrv				/* Physical drive nmuber to identify the drive */
)
{
  disk.is_initialized[pdrv] = 0;
}

Add this function to f_mount, to call it when unmounting a disk.
See in the code STM32f4-discovery.

Tutorial: SD card over SPI using STM32CubeIDE and FatFS
Reference :
https://01001000.xyz/2020-08-09-Tutorial-STM32CubeIDE-SD-card/
