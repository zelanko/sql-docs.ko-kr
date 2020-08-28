---
description: RDS 메서드
title: RDS 메서드 | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: 8403881e3e25f612ac9a27a798ad2d88f192d5cd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981644"
---
# <a name="rds-methods"></a>RDS 메서드
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
|방법|설명|  
|-|-|  
|[취소 (RDS)](./cancel-method-rds.md)|보류 중인 비동기 메서드 호출의 실행을 취소 합니다.|  
|[CancelUpdate (RDS)](./cancelupdate-method-rds.md)|**레코드 집합** 개체의 현재 또는 새 행에 대 한 변경 내용을 취소 합니다.|  
|[ConvertToString (RDS)](./converttostring-method-rds.md)|**레코드 집합을 레코드** 집합 데이터를 나타내는 MIME 문자열로 변환 합니다.|  
|[CreateObject (RDS)](./createobject-method-rds.md)|대상 비즈니스 개체에 대 한 프록시를 만들어 해당 개체에 대 한 포인터를 반환 합니다.|  
|[CreateRecordset (RDS)](./createrecordset-method-rds.md)|연결 되지 않은 빈 **레코드 집합**을 만듭니다.|  
|[Execute 메서드(RDS)](./execute-method-rds.md)|요청을 실행 하 고 고급 데이터 행 집합을 만듭니다 (ADO 2.5 이상에서 사용).|  
|[Execute21 메서드(RDS)](./execute21-method-rds.md)|요청을 실행 하 고 고급 데이터 행 집합을 만듭니다 (ADO 2.1에서 사용).|  
|[InvokeService(RDS)](./invokeservice-rds.md)|개체의 지원 되는 버전에서 요청 된 인터페이스에 대 한 포인터를 반환 합니다.|  
|[MoveFirst, MoveLast, MoveNext, MovePrevious (RDS)](./movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|지정 된 **레코드 집합** 개체에서 첫 번째, 마지막, 다음 또는 이전 레코드로 이동 합니다.|  
|[쿼리 (RDS)](./query-method-rds.md)|는 유효한 SQL 쿼리 문자열을 사용 하 여 **레코드 집합**을 반환 합니다.|  
|[새로 고침 (RDS)](./refresh-method-rds.md)|**Connect** 속성에 지정 된 데이터 원본을 쿼리하고 쿼리 결과를 업데이트 합니다.|  
|[다시 설정 (RDS)](./reset-method-rds.md)|지정 된 정렬 및 필터 속성을 기반으로 클라이언트 쪽 **레코드 집합**에 대 한 정렬 또는 필터를 실행 합니다.|  
|[SubmitChanges (RDS)](./submitchanges-method-rds.md)|로컬에서 캐시 하 고 업데이트할 수 있는 **레코드 집합** 의 보류 중인 변경 내용을 **Connect** 속성에 지정 된 데이터 원본에 전송 합니다.|  
|[Synchronize 메서드(RDS)](./synchronize-method-rds.md)|지정 된 레코드 집합을 연결 문자열에 지정 된 데이터베이스와 동기화 합니다 (ADO 2.5 이상에서 사용).|  
|[Synchronize21 메서드(RDS)](./synchronize21-method-rds.md)|지정 된 레코드 집합을 연결 문자열에 지정 된 데이터베이스와 동기화 합니다 (ADO 2.1에서 사용).|