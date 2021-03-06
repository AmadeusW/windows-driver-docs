---
title: KSPROPERTY\_AUDIO\_PEAKMETER2
description: Windows 8 introduces the KSPROPERTY\_AUDIO\_PEAKMETER2 property that reports the maximum audio signal level that occurred at a peakmeter node (KSNODETYPE\_PEAKMETER) since the last time the peakmeter node was reset.
ms.assetid: 0A59A482-476D-412C-8D15-D821357C355B
keywords: ["KSPROPERTY_AUDIO_PEAKMETER2 Audio Devices"]
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER2
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

# KSPROPERTY\_AUDIO\_PEAKMETER2


Windows 8 introduces the KSPROPERTY\_AUDIO\_PEAKMETER2 property that reports the maximum audio signal level that occurred at a peakmeter node (KSNODETYPE\_PEAKMETER) since the last time the peakmeter node was reset.

## <span id="ddk_ksproperty_audio_peakmeter2_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER2_KS"></span>


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
<td align="left"><p>No</p></td>
<td align="left"><p>Node via Filter or Pin instance</p></td>
<td align="left">[<strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong>](https://msdn.microsoft.com/library/windows/hardware/ff537145)</td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

The property value (operation data) is of type LONG and specifies the peak sample value at the node. If the peak value is negative, its absolute value is used.

### <span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>Return Value

A KSPROPERTY\_AUDIO\_PEAKMETER2 property request returns STATUS\_SUCCESS to indicate that it has completed successfully. Otherwise, the request returns an appropriate error status code. The following table shows a possible error status code.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Status Code</th>
<th align="left">Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>The KS filter cannot return the current value of the peakmeter.</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

The KSPROPERTY\_AUDIO\_PEAKMETER2 property is almost identical to the [**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md) property. The KSPROPERTY\_AUDIO\_PEAKMETER2 property was introduced with Windows 8 and later operating systems to provide improved hardware metering of a pin topology. The legacy KSPROPERTY\_AUDIO\_PEAKMETER property has been retained for backward compatibility.

SignedMinimum must be set to LONG\_MIN (instead of 0x8000), and SignedMaximum must be set to LONG\_MAX (instead of 0x7fff). And also, note that peak meter values are relative to this scale and the scale is linear in amplitude.

So if, for example, you have a waveform with negative and positive peaks at -1 and +1 respectively (on a scale that goes from -1 to +1), then a peak meter value of LONG\_MAX accurately reports the maximum waveform value for a given time window. Conversely, a peak meter value of zero (0) should be used to report silence, where all the waveform’s values are zero. But in the case of a waveform whose peak values are *between* zero (0) and LONG\_MAX, the reported waveform values would be linearly reduced from the originals.

Therefore, in the case of the waveform that swings between -0.5 and +0.5 (on a scale that goes from -1 to +1), the peak meter value must be set to LONG\_MAX/2.

A KS audio filter handles this property request synchronously. If the request succeeds, it resets the peakmeter, which initializes the accumulated peak value to zero. If the request does not succeed, the peakmeter is not changed.

The system sends an IOCTL\_KS\_PROPERTY request for the KSPROPERTY\_AUDIO\_PEAKMETER property at IRQL PASSIVE\_LEVEL.

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](ksproperty-audio-peakmeter.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20KSPROPERTY_AUDIO_PEAKMETER2%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





