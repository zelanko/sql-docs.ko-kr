---
description: ADOX 개체
title: ADOX 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: ca5131235b4c34c05f4cc3b783087f25dc027e95
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771582"
---
# <a name="adox-objects"></a>ADOX 개체
## <a name="adox-object-summary"></a>ADOX 개체 요약  
  
|Object|설명|  
|------------|-----------------|  
|[카탈로그](./catalog-object-adox.md)|데이터 원본의 스키마 카탈로그를 설명 하는 컬렉션을 포함 합니다.|  
|[열](./column-object-adox.md)|테이블, 인덱스 또는 키에서 열을 나타냅니다.|  
|[그룹](./group-object-adox.md)|보안 데이터베이스 내에서 액세스 권한이 있는 그룹 계정을 나타냅니다.|  
|[Index](./index-object-adox.md)|데이터베이스 테이블의 인덱스를 나타냅니다.|  
|[Key](./key-object-adox.md)|데이터베이스 테이블의 기본 키, 외래 키 또는 고유 키 필드를 나타냅니다.|  
|[여기서](./procedure-object-adox.md)|저장 프로시저를 나타냅니다.|  
|[테이블](./table-object-adox.md)|열, 인덱스 및 키를 포함 하는 데이터베이스 테이블을 나타냅니다.|  
|[사용자](./user-object-adox.md)|보안 데이터베이스 내에서 액세스 권한이 있는 사용자 계정을 나타냅니다.|  
|[보기](./view-object-adox.md)|레코드 또는 가상 테이블의 필터링 된 집합을 나타냅니다.|  
  
 이러한 개체 간의 관계는 [ADOX 개체 모델](./adox-object-model.md)에 나와 있습니다.  
  
 각 개체는 해당 컬렉션에 포함 될 수 있습니다. 예를 들어 **Table** 개체는 [Tables](./tables-collection-adox.md) 컬렉션에 포함 될 수 있습니다. 자세한 내용은 [ADOX](./adox-collections.md) 컬렉션 또는 특정 컬렉션 항목을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ADOX API 참조](./adox-object-model.md?view=sql-server-ver15)   
 [ADOX 컬렉션](./adox-collections.md)   
 [ADOX 개체 모델](./adox-object-model.md)   
 [데이터 정의 언어 및 보안을 위한 ADO 확장(ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)