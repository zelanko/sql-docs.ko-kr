---
description: ADO 개체 및 컬렉션
title: ADO 개체 및 컬렉션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: rothja
ms.author: jroth
ms.openlocfilehash: 101eab85f19922b56a7e7f86f330188d87fcc9fe
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806417"
---
# <a name="ado-objects-and-collections"></a>ADO 개체 및 컬렉션
ADO는 다음 9 개의 개체와 4 개의 컬렉션으로 구성 됩니다.  
  
|개체 또는 컬렉션|설명|  
|--------------------------|-----------------|  
|**Connection** 개체|데이터 원본의 고유 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템의 경우 서버에 대 한 실제 네트워크 연결에 해당 하는 것일 수 있습니다. 공급자가 지 원하는 기능에 따라 **연결** 개체의 일부 컬렉션, 메서드 또는 속성을 사용 하지 못할 수 있습니다.|  
|**Command** 개체|데이터 원본에 대해 실행 하기 위한 SQL 쿼리와 같은 특정 명령을 정의 하는 데 사용 됩니다.|  
|**레코드 집합** 개체|기본 테이블의 전체 레코드 집합 또는 실행 된 명령의 결과를 나타냅니다. 모든 **레코드 집합** 개체는 레코드 (행)와 필드 (열)로 구성 됩니다.|  
|**Record** 개체|**레코드 집합** 또는 공급자에서 데이터의 단일 행을 나타냅니다. 이 레코드는 공급자에 따라 데이터베이스 레코드 또는 파일 또는 디렉터리와 같은 다른 유형의 개체를 나타낼 수 있습니다.|  
|**Stream** 개체|이진 또는 텍스트 데이터의 스트림을 나타냅니다. 예를 들어 XML 문서를 명령 입력에 대 한 스트림으로 로드 하거나 특정 공급자에서 쿼리 결과로 반환할 수 있습니다. **Stream** 개체는 이러한 데이터 스트림을 포함 하는 필드나 레코드를 조작 하는 데 사용할 수 있습니다.|  
|**Parameter** 개체|매개 변수가 있는 쿼리 또는 저장 프로시저를 기반으로 **Command** 개체와 연결 된 매개 변수 또는 인수를 나타냅니다.|  
|**Field** 개체|공통 데이터 형식으로 데이터의 열을 나타냅니다. 각 **Field** 개체는 **레코드 집합**의 열에 해당 합니다.|  
|**Property** 개체|공급자에 의해 정의 되는 ADO 개체의 특징을 나타냅니다. ADO 개체에는 기본 제공 및 동적 속성의 두 가지 유형이 있습니다. 기본 제공 속성은 ADO에서 구현 되 고 모든 새 개체에서 즉시 사용할 수 있는 속성입니다. **속성** 개체는 기본 공급자가 정의 하는 동적 속성의 컨테이너입니다.|  
|**Error** 개체|공급자와 관련 된 단일 작업과 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.|  
|**Fields** 컬렉션|**레코드 집합** 또는 **Record** 개체의 모든 **필드** 개체를 포함 합니다.|  
|**Properties** 컬렉션|개체의 특정 인스턴스에 대 한 모든 **속성** 개체를 포함 합니다.|  
|**Parameters** 컬렉션|**Command** 개체의 모든 **Parameter** 개체를 포함 합니다.|  
|**Errors** 컬렉션|단일 공급자 관련 오류에 대 한 응답으로 생성 된 모든 **오류** 개체를 포함 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADO 개체 모델](../../reference/ado-api/ado-object-model.md)