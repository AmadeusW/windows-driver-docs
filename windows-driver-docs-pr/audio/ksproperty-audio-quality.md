---
title: KSPROPERTY\_AUDIO\_QUALITY
description: The KSPROPERTY\_AUDIO\_QUALITY property specifies the quality level of a node's output stream. This is a property of an SRC node (KSNODETYPE\_SRC).
ms.assetid: ef57de3b-f7ac-4ecd-915e-27f34fcc2028
keywords: ["KSPROPERTY_AUDIO_QUALITY Audio Devices"]
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# KSPROPERTY\_AUDIO\_QUALITY


The KSPROPERTY\_AUDIO\_QUALITY property specifies the quality level of a node's output stream. This is a property of an SRC node ([**KSNODETYPE\_SRC**](ksnodetype-src.md)).

## <span id="ddk_ksproperty_audio_quality_ks"></span><span id="DDK_KSPROPERTY_AUDIO_QUALITY_KS"></span>


### <span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>Usage Summary Table

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">Set</th>
<th align="left">Target</th>
<th align="left">Property descriptor type</th>
<th align="left">Property value type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Yes</p></td>
<td align="left"><p>Yes</p></td>
<td align="left"><p>Pin</p></td>
<td align="left">[<strong>KSNODEPROPERTY</strong>](https://msdn.microsoft.com/library/windows/hardware/ff537143)</td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

The property value (operation data) is of type ULONG and indicates the output stream's quality level. This value should be set to one of the following constants from header file Ksmedia.h:

<span id="KSAUDIO_QUALITY_WORST"></span><span id="ksaudio_quality_worst"></span>KSAUDIO\_QUALITY\_WORST  
Worst quality

<span id="KSAUDIO_QUALITY_PC"></span><span id="ksaudio_quality_pc"></span>KSAUDIO\_QUALITY\_PC  
Standard computer quality (with no constraints)

<span id="KSAUDIO_QUALITY_BASIC"></span><span id="ksaudio_quality_basic"></span>KSAUDIO\_QUALITY\_BASIC  
Basic (low-end) consumer audio quality (default value)

<span id="KSAUDIO_QUALITY_ADVANCED"></span><span id="ksaudio_quality_advanced"></span>KSAUDIO\_QUALITY\_ADVANCED  
Advanced (high-end) consumer audio quality

### <span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>Return Value

A KSPROPERTY\_AUDIO\_QUALITY property request returns STATUS\_SUCCESS to indicate that it has completed successfully. Otherwise, the request returns an appropriate error status code.

Remarks
-------

For information about the types of sample-rate conversion that the [KMixer system driver](https://msdn.microsoft.com/library/windows/hardware/ff537039#kmixer-system-driver) performs, see [KMixer Driver Sample Rate Conversion and Mixing Policy](https://msdn.microsoft.com/library/windows/hardware/ff537047).

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
<td align="left">Ksmedia.h (include Ksmedia.h)</td>
</tr>
</tbody>
</table>

## <span id="see_also"></span>See also


[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20KSPROPERTY_AUDIO_QUALITY%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





