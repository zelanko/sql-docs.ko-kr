---
title: "INDEX 명령 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40581a79d22feadb8616c021820e93a634ef94d7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="index-command"></a>INDEX 명령
표시 하 고 액세스할 논리적 순서에 따라 테이블 레코드 인덱스 파일을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>인수  
 *eExpression*  
 현재 테이블에서 필드의 이름을 포함할 수 있는 인덱스 식을 지정 합니다. 인덱스 식을 기반으로 하는 인덱스 키 테이블의 각 레코드에 대 한 인덱스 파일에 만들어집니다. Visual FoxPro 이러한 키를 사용 하 여 표시 하 고 테이블의 레코드에 액세스 합니다.  
  
> [!NOTE]  
>  권장 되지는 않지만 *eExpression* 메모리 변수, 배열 요소 또는 필드 또는 다른 작업 영역에 테이블에서 필드 식을 수도 있습니다. 인덱스 파일 식; 단독 메모 필드를 사용할 수 없습니다. 문자 식이 다른 식 결합 해야 합니다. Visual FoxPro 변수 또는 필드를 더 이상 존재 하지 않거나 찾을 수 없습니다. 포함 하는 인덱스를 액세스 하는 경우 오류 메시지를 생성 합니다.  
  
 길이에 따라 다른 키와 인덱스를 작성 하려고 하면 키 공백으로 채워집니다. 가변 길이 인덱스 키 Visual FoxPro에 지원 되지 않습니다.  
  
 길이가 0 인 인덱스 키를 만들 수는 있습니다. 예를 들어 0 길이 인덱스 키 인덱스 식이 빈 메모 필드의 부분 문자열 때 만들어집니다. 0 길이 인덱스 키에는 오류 메시지를 생성 합니다. Visual FoxPro 인덱스를 만들면 테이블의 첫 번째 레코드의 필드를 평가 합니다. 필드가 비어 있으면 임시 데이터를 길이가 0 인 인덱스 키를 방지 하기 위해 첫 번째 레코드의 필드에 입력 해야 할 수도 있습니다.  
  
 *IDXFileName*  
 .Idx 인덱스 파일을 만듭니다. 인덱스 파일에는 기본 확장.idx를 지정 됩니다.  
  
 태그 *TagName*[OF *CDXFileName*]  
 복합 인덱스 파일을 만듭니다. 복합 인덱스 파일이 별도 태그 (인덱스 항목)을 개수에 관계 없이 구성 된 단일 인덱스 파일입니다. 각 태그는 고유 태그 이름으로 식별 됩니다. 태그 이름은 문자 또는 밑줄로 시작 해야 하며 최대 10 개의 문자, 숫자 또는 밑줄 조합이 될 수 있습니다. 복합 인덱스 파일의 태그의 수는 사용 가능한 메모리 및 디스크 공간에 의해서만 제한 됩니다.  
  
 복합 인덱스를 여러 입력 파일을 압축 항상 합니다. 복합 인덱스 파일을 만들 때 압축을 포함할 필요가 없습니다. 복합 인덱스 파일의 이름은.cdx 확장을 제공 됩니다.  
  
 두 가지 유형의 복합 인덱스 파일을 만들 수 있습니다: 구조적 및 비구조적 인 합니다.  
  
 **구조적 복합 인덱스 파일** 태그와 구조 복합 인덱스 파일을 만들 수 있습니다 *TagName* 선택적 OF를 제외 하 여 *CDXFileName* 절. 항상 구조적 복합 인덱스 파일은 테이블과 동일한 기본 이름을 하 게 되 고 테이블을 열 때 자동으로 열립니다.  
  
 **비구조적 인 복합 인덱스 파일** OF를 포함 하 여 비구조적 인 복합 인덱스 파일을 만들 수 있습니다 *CDXFileName* 태그 뒤 *TagName*합니다. 구조적 복합 인덱스 파일과 달리 비구조적 인 복합 인덱스 파일이 사용 중인 인덱스 절과 함께 명시적으로 열려 있어야 합니다.  
  
 복합 인덱스 파일이 이미 생성 되어 열, 하는 경우 발급 태그로 인덱스 *TagName* 복합 인덱스 파일에 태그를 추가 합니다.  
  
 에 대 한 *lExpression*  
 그에 따라 조건을 지정 필터 식을 만족 하는 레코드만 *lExpression* 표시 및 액세스;에 사용할 수 있는 인덱스 키는 필터 식과 일치 하는 해당 레코드에 대 한 인덱스 파일에서 생성 됩니다.  
  
 Visual FoxPro Rushmore 기술 최적화 인덱스 중... 에 대 한 *lExpression* 경우 명령 *lExpression* 최적화할 수 있는 식입니다. 최상의 성능을 최적화할 수 있는 식을 FOR 절에 사용 합니다.  
  
 압축  
 Compact.idx 파일을 만듭니다.  
  
 오름차순  
 오름차순.cdx 파일에 대 한을 지정합니다. 기본적으로 오름차순.cdx 태그 만들어집니다. (오름차순 인덱스 파일의 주문의 포함할 수 있습니다.) 내림차순을 포함 하 여 테이블을 역순으로 인덱싱할 수 있습니다.  
  
 내림차순  
 .Cdx 파일에 대 한 내림차순을 지정 합니다. .Idx 인덱스 파일을 만들 때 내림차순을 포함할 수 없습니다.  
  
 UNIQUE  
 특정 인덱스 키 값으로 발생 하는 첫 번째 레코드만.idx 파일이 나.cdx 태그에 포함 되어 있는지를 지정 합니다. UNIQUE 중복 레코드를 표시 또는 액세스를 방지 하기 위해 사용할 수 있습니다. 중복 인덱스 키를 가진 추가 된 모든 레코드는 인덱스 파일에서 제외 됩니다. 인덱스의 고유한 옵션을 사용 하 여 인덱스 또는 다시 인덱싱을 실행 하기 전에 SET UNIQUE ON을 실행 하는 것과 결과가 같습니다.  
  
 고유 인덱스 또는 인덱스 태그가 활성 상태일 때 중복 된 레코드는 해당 인덱스 키를 변경 하는 방식으로 변경 되는 인덱스 또는 인덱스 태그 업데이트 됩니다. 그러나 원래 인덱스 키와 다음 중복 된 레코드에 액세스 하거나 인덱스를 사용 하 여 파일 재 색인 될 때까지 표시 수 없습니다.  
  
 후보  
 후보 구조적 인덱스 태그를 만듭니다. 후보 키워드; 구조적 인덱스 태그를 만들 때만 포함 될 수 있습니다. 그렇지 않으면 Visual FoxPro 오류 메시지를 생성 합니다.  
  
 필드 또는 조합 된 인덱스 식에 지정 된 필드에 중복 값을 방지 하는 후보 인덱스 태그 *eExpression*합니다. 용어 *후보* 인덱스;의 형식을 참조 기본 인덱스가 되기 위해 "대상"으로 자격이 후보 인덱스에 중복 값 인해 합니다.  
  
 Visual FoxPro 필드나 이미 중복 값을 포함 하는 필드의 조합에 대 한 후보 인덱스 태그를 만드는 경우에 오류가 발생 합니다.  
  
 가감 연산자  
 유지는 모든 이전에 열린된 인덱스 파일을 엽니다. 인덱스와 인덱스 파일 또는 테이블에 대 한 파일을 만들 때 덧셈 절을 생략 하면 (구조적 복합 인덱스)를 제외한 모든 이전에 열린된 인덱스 파일이 닫힙니다.  
  
## <a name="remarks"></a>주의  
 인덱스 파일이 있는 테이블의에서 레코드에 표시 되 고 인덱스 식으로 지정 된 순서 대로 액세스 합니다. 테이블의 레코드의 물리적 순서는 인덱스 파일이 변경 되지 않습니다.  
  
## <a name="index-types"></a>인덱스 유형  
 Visual FoxPro를 사용 하면 두 가지 유형의 인덱스 파일을 만들 수 있습니다.  
  
-   복합 태그 라고 부르는 여러 인덱스 항목이 포함 되도록.cdx 인덱스 파일  
  
-   하나의 인덱스 항목을 포함 하는.idx 인덱스 파일  
  
 또한 테이블과 함께 자동으로 열리는 구조적 복합 인덱스 파일을 만들 수 있습니다.  
  
> [!NOTE]  
>  구조적 복합 인덱스 파일은 테이블을 열 때 자동으로 열립니다, 때문에 기본 인덱스 유형 됩니다.  
  
 압축 파일을 만드는 compact.idx 인덱스를 포함 합니다. 복합 인덱스 파일을 압축 항상 합니다.  
  
## <a name="index-order-and-updating"></a>인덱스 순서 및 업데이트  
 인덱스는 하나만 파일 (마스터 인덱스 파일) 또는 태그 (마스터 태그)는 테이블 표시 되 나 액세스 순서를 제어 합니다. 특정 명령 (예:: SEEK) 마스터 인덱스 파일이 나 태그를 사용 하 여 레코드를 검색 합니다. 그러나 모든.idx 열고 테이블에 변경 내용이.cdx 인덱스 파일이 업데이트 됩니다.  
  
## <a name="user-defined-functions"></a>사용자 정의 함수  
 인덱스 식에서 사용자 정의 함수를 포함할 수 있지만 인덱스 식에 사용자 지정 기능을 사용 하지 않아야 합니다. 인덱스 식의 사용자 정의 함수 만들기 또는 인덱스를 업데이트 하는 데 걸리는 시간을 늘립니다. 또한 사용자 정의 함수는 인덱스 식에 사용 되는 경우 인덱스 업데이트가 발생 하지 수도 있습니다.  
  
 인덱스 식에는 사용자 정의 함수를 사용 하는 경우 Visual FoxPro 사용자 정의 함수를 찾을 수 있어야 합니다. Visual FoxPro 인덱스를 만들면 인덱스 식이 인덱스 파일에 저장 되지만 인덱스 식에 사용자 정의 함수에 대 한 참조만 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [태그 명령 삭제](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 명령](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 명령](../../odbc/microsoft/set-unique-command.md)
