---
title: "ADO 개체 및 컬렉션 | Microsoft Docs"
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
helpviewer_keywords: ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b2bd4d1caf6ad0f2b180804407aede35155208e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-objects-and-collections"></a>ADO 개체 및 컬렉션
ADO는 다음 9 개의 개체와 4 개의 컬렉션으로 이루어져 있습니다.  
  
|개체 또는 컬렉션|Description|  
|--------------------------|-----------------|  
|**연결** 개체|데이터 원본의 고유 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템의 경우에 실제 네트워크 연결 서버에 해당 수도 있습니다. 공급자, 일부 컬렉션, 메서드 또는 속성을 지 원하는 기능에 따라 한 **연결** 개체를 사용할 수 없습니다.|  
|**Command** 개체|데이터 원본에 대해 실행 하려는 SQL 쿼리를 같은 특정 명령을 정의 하는 데 사용 합니다.|  
|**레코드 집합** 개체|기본 테이블이 나 실행 된 명령의 결과에서 레코드의 전체 집합을 나타냅니다. 모든 **레코드 집합** 개체 레코드 (행)으로 구성 하 고 필드 (열)입니다.|  
|**레코드** 개체|데이터의 단일 행을 나타냅니다는 **레코드 집합** 또는 공급자에서 합니다. 이 레코드는 데이터베이스 레코드 또는 기타 다른 유형의 파일 또는 디렉터리를 공급자에 따라 같은 개체를 나타낼 수 있습니다.|  
|**스트림** 개체|이진 또는 텍스트 데이터의 스트림을 나타냅니다. 예를 들어, 입력 또는 쿼리의 결과로 특정 공급자에서 반환 된 명령에 대 한 스트림으로 XML 문서를 로드할 수 있습니다. A **스트림** 파일이 나 이러한 스트림에 데이터를 포함 하는 레코드 개체를 사용할 수 있습니다.|  
|**매개 변수** 개체|매개 변수 또는 연결 된 인수를 나타냅니다는 **명령** 매개 변수가 있는 쿼리 또는 저장된 프로시저에 따라 개체를 합니다.|  
|**필드** 개체|일반 데이터 형식과 데이터의 열을 나타냅니다. 각 **필드** 의 열에 해당 하는 개체는 **레코드 집합**합니다.|  
|**속성** 개체|공급자에 의해 정의 된 ADO 개체의 특성을 나타냅니다. ADO 개체에는 두 가지 유형의 속성: 기본 제공 및 동적입니다. 기본 제공 속성은 ado에서 및 모든 새 개체를 즉시 사용할 수 있는 구현 된 속성입니다. **속성** 개체는 기본 공급자가 정의 하는 동적 속성에 대 한 컨테이너입니다.|  
|**Error** 개체|공급자 관련 단일 작업에 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.|  
|**필드** 컬렉션|모든 포함 된 **필드** 의 개체는 **레코드 집합** 또는 **레코드** 개체입니다.|  
|**속성** 컬렉션|모든 포함 된 **속성** 개체의 특정 인스턴스에 대 한 개체입니다.|  
|**매개 변수** 컬렉션|모든 포함 된 **매개 변수** 의 개체는 **명령** 개체입니다.|  
|**오류** 컬렉션|모든 포함 된 **오류** 단일 공급자 관련 오류에 대 한 응답에서 생성 된 개체입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)
