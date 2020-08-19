---
description: IDSOShapeExtensions 인터페이스
title: IDSOShapeExtensions 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c7eeb5999a42cfe8b82e570cc5ada1222f87441
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443475"
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions 인터페이스
셰이프 공급자에 대 한 내부 OLE DB 데이터 소스 개체를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|-|-|  
|[GetDataProviderDSO 메서드](../../../ado/reference/ado-api/getdataproviderdso-method.md)|셰이프 공급자에서 내부 OLE DB 데이터 소스 개체를 검색 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
