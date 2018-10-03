---
title: DCOM Stream 마샬링 형식 설정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33359afb2910c75e34ff38c9606ff71b3760cbc1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802861"
---
# <a name="setting-dcom-stream-marshaling-format"></a>DCOM 스트림 마샬링 형식 설정
RDS 1.5 또는 이전 구성 요소를 사용 하 여 클라이언트 컴퓨터에서 RDS 2.0 이상을 구성 요소를 사용 하 여 서버와 호환 되지 않습니다. DCOM을 사용 하 여 기본 프로토콜로 때 이상 RDS 2.0에 대 한 지원이 더욱 효율적으로 전송 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 클라이언트 구성 요소에서 RDS 1.5 또는 이전 버전을 실행 중인 경우에 이전 RDS 지원 (RDS 1.0 이라고 함) 또는 최신 RDS 지원 호출된 RDS (2.0 이상)를 사용 하 여 서버를 설정할 수 있습니다. 다음 레지스트리 항목을 중 하나를 설정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -또는-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


