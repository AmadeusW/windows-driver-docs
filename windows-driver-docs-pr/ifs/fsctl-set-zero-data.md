---
title: FSCTL\_SET\_ZERO\_DATA control code
description: The FSCTL\_SET\_ZERO\_DATA control code fills a specified range of a file with zeros (0).
ms.assetid: AEC4DAD4-17EB-412B-881B-E54F6A578637
keywords: ["FSCTL_SET_ZERO_DATA control code Installable File System Drivers"]
topic_type:
- apiref
api_name:
- FSCTL_SET_ZERO_DATA
api_location:
- ntifs.h
api_type:
- HeaderDef
---

# FSCTL\_SET\_ZERO\_DATA control code


The **FSCTL\_SET\_ZERO\_DATA** control code fills a specified range of a file with zeros (0). If the file is sparse or compressed, the NTFS file system may deallocate disk space in the file. This sets the range of bytes to zeros (0) without extending the file size.

To perform this operation from a driver, call [**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988) with the following parameters.

**Parameters**

<a href="" id="instance"></a>*Instance*  
Opaque instance pointer for the caller. This parameter is required and cannot be **NULL**.

<a href="" id="fileobject"></a>*FileObject*  
File object pointer to the file in which to write zeros to. This parameter is required and cannot be **NULL**.

<a href="" id="fscontrolcode"></a>*FsControlCode*  
The control code for the operation.

Use **FSCTL\_SET\_ZERO\_DATA** for this operation.

<a href="" id="inputbuffer"></a>*InputBuffer*  
A pointer to a [**FILE\_ZERO\_DATA\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/mt668763) or [**FILE\_ZERO\_DATA\_INFORMATION\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt668764) structure that specifies the range of the file to set to zeros.

The **FileOffset** member is the byte offset of the first byte to set to zeros (0), and the **BeyondFinalZero** member is the byte offset of the first byte beyond the last zero (0) byte.

The **Flags** member in [**FILE\_ZERO\_DATA\_INFORMATION\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt668764) specifies modifiers to the operation. For example, when **Flags** is set to **FILE\_ZERO\_DATA\_INFORMATION\_FLAG\_PRESERVE\_CACHED\_DATA**, the contents of the cache corresponding to this range of the file are not purged.

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
The size of the input buffer, in bytes.

<a href="" id="outputbuffer"></a>*OutputBuffer*  
Not used with this operation; set to **NULL**.

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
Not used with this operation; set to zero.

Status block
------------

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988) returns **STATUS\_SUCCESS** or an appropriate NTSTATUS value.

-   **STATUS \_INSUFFICIENT\_RESOURCES** is returned when there is not enough memory to complete the operation.
-   **STATUS\_INVALID\_PARAMETER** is returned when the *InputBufferLength* is smaller than the size of the **FILE\_ZERO\_DATA\_INFORMATION** structures or the file specified is a system metadata file or a directory.
-   **STATUS\_ACCESS\_DENIED** is returned when the **FILE\_ZERO\_DATA\_INFORMATION\_FLAG\_PRESERVE\_CACHED\_DATA** is set from user mode.
-   **STATUS\_MEDIA\_WRITE\_PROTECTED** is returned if the volume is currently write protected.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (include Ntifs.h)</td>
</tr>
</tbody>
</table>

## See also


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FILE\_ZERO\_DATA\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/mt668763)

[**FILE\_ZERO\_DATA\_INFORMATION\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt668764)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bifsk\ifsk%5D:%20FSCTL_SET_ZERO_DATA%20control%20code%20%20RELEASE:%20%281/9/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





