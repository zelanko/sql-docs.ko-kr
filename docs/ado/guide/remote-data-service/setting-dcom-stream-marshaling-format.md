---
description: DCOM 스트림 마샬링 형식 설정
title: DCOM 스트림 마샬링 형식 설정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: rothja
ms.author: jroth
ms.openlocfilehash: 42d49824bc814026348c6f3aef99860b40f20f76
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759263"
---
# <a name="setting-dcom-stream-marshaling-format"></a>DCOM 스트림 마샬링 형식 설정
RDS 1.5 또는 이전 버전의 구성 요소를 사용 하는 클라이언트 컴퓨터는 RDS 2.0 이상에서 구성 요소를 사용 하는 서버와 호환 되지 않습니다. DCOM을 기본 프로토콜로 사용할 때 RDS 2.0 이상에 대 한 지원은 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 전송 하는 데 더 효율적입니다. 클라이언트가 RDS 1.5 이전 버전의 구성 요소를 실행 하는 경우 이전 RDS 지원 (RDS 1.0 이라고 함) 또는 최신 RDS 지원 (RDS 2.0 이상)을 사용 하도록 서버를 설정할 수 있습니다. 다음 레지스트리 항목 중 하나를 설정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 또는  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```