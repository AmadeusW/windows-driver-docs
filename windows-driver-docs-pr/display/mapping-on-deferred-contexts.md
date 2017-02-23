---
title: Mapping on Deferred Contexts
description: Mapping on Deferred Contexts
ms.assetid: 29c44639-ea5e-4255-8e8c-f6d5e3af0dfb
keywords: ["Direct3D version 11 WDK Windows 7 display , deferred contexts, mapping", "Direct3D version 11 WDK Windows Server 2008 R2 display , deferred contexts, mapping", "mapping on deferred contexts WDK Windows 7 display", "mapping on deferred contexts WDK Windows Server 2008 R2 display , excluding DDI functions", "deferred contexts WDK Windows 7 display , mapping", "deferred contexts WDK Windows Server 2008 R2 display , mapping"]
---

# Mapping on Deferred Contexts


This section applies only to Windows 7 and later, and Windows Server 2008 R2 and later versions of Windows operating system.

The runtime can map a dynamic resource (through a call to the driver's [**ResourceMap**](https://msdn.microsoft.com/library/windows/hardware/ff569492) function) on a deferred context, as the Direct3D version 11 API ensures that the first use of the mapped dynamic resource is to discard the previous contents. The best option is to create a new dynamic resource on each discard over continually using the original dynamic resource. The creation of this aliased resource is required to allow operations that are done to the virtual dynamic resource in the timeline of the deferred context to not affect the operations that are done to the virtual dynamic resource in the timeline of the immediate context. Remember, that deferred contexts are merely recording operations that eventually are actualized during a call to the driver's [**CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476) function. When a dynamic resource is used, the original intentions of the application are preserved, and write-combined GPU-accessible memory is provided to the application (that is, the memory is optimized for single-use CPU upload).

Each resource map can provide the pointers directly to the aliased resource. There is an additional burden on deferred context recording to implement this type of aliasing. For example, deferred context recording might require new views to be created for aliased textures. Integrations with driver aliasing are necessary and seem plausible to do. When a command list is executed, the last context-local created resource (to satisfy the map-discard calls) must be substituted as the "current" resource that backs the dynamic resource for the immediate context, and so on.

A call to the driver's [**ResourceCopy**](https://msdn.microsoft.com/library/windows/hardware/ff569489) function to copy a resource to a dynamic resource must still be supported both on the deferred context, after map-discard calls, and on the immediate context after a call to the driver's [**CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476) function, where the local deferred context resource is ideally swapped into the immediate context version of the "current" resource. A call to the driver's **ResourceCopy** function with dynamic-resource destinations is not frequently used, so you should use a copy-on-write mechanism. If **ResourceCopy** is called that would affect either the dynamic resource on the deferred context after a map-discard call or on the immediate context that holds a command list local resource as current, a new resource should be conceptually allocated to provide the new destination of the copy, and the old resource must be copied to the new resource (if the operation is a [**ResourceCopyRegion**](https://msdn.microsoft.com/library/windows/hardware/ff569490)).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Mapping%20on%20Deferred%20Contexts%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



