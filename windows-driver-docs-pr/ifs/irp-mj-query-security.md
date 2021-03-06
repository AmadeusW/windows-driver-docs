---
title: IRP\_MJ\_QUERY\_SECURITY
description: IRP\_MJ\_QUERY\_SECURITY
ms.assetid: f0f73bfe-c016-49e2-b725-380f46a9b9d6
keywords: ["IRP_MJ_QUERY_SECURITY Installable File System Drivers"]
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_SECURITY
api_type:
- NA
---

# IRP\_MJ\_QUERY\_SECURITY


## When Sent


The IRP\_MJ\_QUERY\_SECURITY request is sent by the I/O Manager. It can be sent, for example, when a user-mode application has called a Microsoft Win32 function such as **GetSecurityInfo**.

## <a href="" id="operation-fsd"></a>Operation: File System Drivers


The file system driver should extract and decode the file object to determine whether it represents a user file or directory open. If it does, the driver should process the query and complete the IRP. Otherwise, the driver should complete the IRP as appropriate without processing the query.

## <a href="" id="operation-filter"></a>Operation: File System Filter Drivers


The filter driver should pass this IRP down to the next-lower driver on the stack.

## Parameters


A file system or filter driver calls [**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174) with the given IRP to get a pointer to its own [**stack location**](https://msdn.microsoft.com/library/windows/hardware/ff550659) in the IRP, shown in the following list as *IrpSp*. (The IRP is shown as *Irp*.) The driver can use the information that is set in the following members of the IRP and the IRP stack location in processing a query security request:

<a href="" id="deviceobject"></a>*DeviceObject*  
A pointer to the target device object.

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
A pointer to an [**IO\_STATUS\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff550671) structure that receives the final completion status and information about the requested operation.

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
A pointer to a caller-supplied output buffer that receives a copy of the security descriptor of the specified object. The calling process must have the right to view the specified aspects of the object's security status. The [**SECURITY\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/ff556610) structure is returned in self-relative format.

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
A pointer to the file object that is associated with *DeviceObject*.

On Windows XP and later, the file object can represent a named data stream. For more information about named data streams, see [**FILE\_STREAM\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff540364).

The *IrpSp-&gt;FileObject* parameter contains a pointer to the **RelatedFileObject** field, which is also a FILE\_OBJECT structure. The **RelatedFileObject** field of the FILE\_OBJECT structure is not valid during the processing of IRP\_MJ\_QUERY\_SECURITY and should not be used.

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
Specifies IRP\_MJ\_QUERY\_SECURITY.

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp-&gt;Parameters.QuerySecurity.Length*  
The size, in bytes, of the buffer pointed to by the *Irp-&gt;UserBuffer* parameter.

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp-&gt;Parameters.QuerySecurity.SecurityInformation*  
A pointer to the [**SECURITY\_INFORMATION**](security-information.md) structure for the operation.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation Value</th>
<th align="left">Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>Indicates that the owner identifier of the object is being queried. Requires READ_CONTROL access.</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>Indicates that the primary group identifier of the object is being queried. Requires READ_CONTROL access.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>Indicates that the discretionary access control list (DACL) of the object is being queried. Requires READ_CONTROL access.</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>Indicates that the system ACL (SACL) of the object is being queried. Requires ACCESS_SYSTEM_SECURITY access.</p></td>
</tr>
</tbody>
</table>

 

## See also


[**FILE\_STREAM\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**IO\_STACK\_LOCATION**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_STATUS\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_SECURITY**](irp-mj-set-security.md)

[**SECURITY\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**SECURITY\_INFORMATION**](security-information.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bifsk\ifsk%5D:%20IRP_MJ_QUERY_SECURITY%20%20RELEASE:%20%281/9/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





