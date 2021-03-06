---
UID: NC:d3dumddi.PFND3DDDI_OFFERALLOCATIONS2CB
title: PFND3DDDI_OFFERALLOCATIONS2CB (d3dumddi.h)
description: Called by the user-mode display driver to offer video memory allocations for reuse.
old-location: display\pfnofferallocations2cb.htm
tech.root: display
ms.assetid: 4A8123D3-3A7D-4716-BD02-DD6533DB22F6
ms.date: 05/10/2018
ms.keywords: PFND3DDDI_OFFERALLOCATIONS2CB, PFND3DDDI_OFFERALLOCATIONS2CB callback, d3dumddi/pfnOfferAllocations2Cb, display.pfnofferallocations2cb, pfnOfferAllocations2Cb, pfnOfferAllocations2Cb callback function [Display Devices]
ms.topic: callback
req.header: d3dumddi.h
req.include-header: D3dumddi.h
req.target-type: Windows
req.target-min-winverclnt: Windows 10
req.target-min-winversvr: Windows Server 2016
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: 
topic_type:
- APIRef
- kbSyntax
api_type:
- UserDefined
api_location:
- d3dumddi.h
api_name:
- pfnOfferAllocations2Cb
product:
- Windows
targetos: Windows
req.typenames: 
---

# PFND3DDDI_OFFERALLOCATIONS2CB callback function


## -description


Called by the user-mode display driver   to offer  video memory allocations for reuse.


## -parameters




### -param hDevice [in]

A handle to the display device (graphics context). The Direct3D runtime passed the user-mode driver this handle as the <b>hDevice</b> member of the <a href="https://msdn.microsoft.com/library/windows/hardware/ff542931">D3DDDIARG_CREATEDEVICE</a> structure at device creation.


### -param *








*pData* [in]

A pointer to a <a href="https://msdn.microsoft.com/library/windows/hardware/mt761969">D3DDDICB_OFFERALLOCATIONS2</a> structure  that defines the video memory allocations that the driver offers.


## -returns

Returns one of the following values.

| **Return code** | **Description** | 
|:--|:--|
| **S_OK** | The allocations were successfully offered.<br/>**Note:** If the driver does not need to call [pfnOfferAllocations2Cb](https://msdn.microsoft.com/4A8123D3-3A7D-4716-BD02-DD6533DB22F6) , it should return S_OK.| 
| **D3DDDIERR_DEVICEREMOVED** | The video memory manager or display miniport driver could not complete the operation because either a Plug and Play (PnP) Stop event or a Timeout Detection and Recovery (TDR) event occurred.<br/>**Note:** If this error code is returned, the driver's calling function (typically the [pfnOfferResources](https://msdn.microsoft.com/2E85EFB6-6116-4FE7-97E0-547FFD61B511)  routine) must return this error code to the Direct3D runtime. | 
| **E_INVALIDARG** | An invalid parameter was supplied. | 



## -remarks



The user-mode display driver calls <b>pfnOfferAllocations2Cb</b> to notify the Microsoft DirectX graphics kernel subsystem that, after it completes any previously submitted render operations,  it can offer the allocations' memory for other processes to use.

After the driver calls <b>pfnOfferAllocations2Cb</b> to offer an allocation to reuse, it must call <a href="https://msdn.microsoft.com/BA0A8BF0-39C2-4641-9952-05512B1B1662">pfnReclaimAllocations3Cb</a>  before it locks the allocation or submits it for rendering operations.

<b>pfnOfferAllocations2Cb</b> functions identically to <a href="https://msdn.microsoft.com/library/windows/hardware/hh451693">pfnOfferAllocationsCb</a>, except that it takes flags into account through the pData parameter.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff542931">D3DDDIARG_CREATEDEVICE</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/mt761969">D3DDDICB_OFFERALLOCATIONS2</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff544512">D3DDDI_DEVICECALLBACKS</a>



<a href="https://msdn.microsoft.com/2E85EFB6-6116-4FE7-97E0-547FFD61B511">pfnOfferResources</a>



<a href="https://msdn.microsoft.com/BA0A8BF0-39C2-4641-9952-05512B1B1662">pfnReclaimAllocations3Cb</a>
 

 

