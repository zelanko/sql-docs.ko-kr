---
title: "DCOM 스트림 형식 마샬링 설정 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 370958ce7f66aa7a87296f47884b62a08935fae0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-dcom-stream-marshaling-format"></a>설정 DCOM 스트림 형식 마샬링
RDS 1.5에서 또는 이전 버전의 구성 요소를 사용 하는 클라이언트 컴퓨터에서 RDS 2.0 이상을 구성 요소를 사용 하는 서버와 호환 되지 않습니다. RDS 2.0 이상을 지원이 전송에 더 효율적 DCOM을 기본 프로토콜로 사용 하는 경우 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 클라이언트 구성 요소에서 RDS 1.5 또는 이전 버전을 실행 중인 경우에 이전 RDS 지원 (RDS 1.0 이라고 함) 또는 최신 RDS 지원 (2.0 이상 이라는 RDS)을 사용 하 여 서버를 설정할 수 있습니다. 다음 레지스트리 항목 중 하나를 설정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -또는-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


