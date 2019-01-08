---
title: 열 매핑(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 221fdaaeae61b3005fbbe0088ce4270fd4b6c2b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782675"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>열 매핑(SQL Server 가져오기 및 내보내기 마법사)
  사용 된 **열 매핑** 변환 매개 변수를 편집할 대화 상자.  
  
> [!NOTE]  
>  테이블 복사 옵션을 선택할 경우 테이블의 모든 열을 복사하지 않아도 됩니다. 선택  **\<무시 >** 에 **대상** 건너 뛰 려는 열에 대 한이 대화 상자의 열입니다.  
  
 이 마법사에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사를 성공적으로 실행 하는 데 필요한 사용 권한 뿐만 아니라 마법사 시작 옵션을 알아보려면 [SQL Server 가져오기 및 내보내기 마법사를 실행](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **원본**  
 선택한 원본 테이블, 뷰 또는 쿼리를 식별합니다.  
  
 **대상**  
 선택한 대상 테이블, 뷰 또는 쿼리를 식별합니다.  
  
 **대상 테이블/파일 만들기**  
 대상 테이블이 없는 경우 이를 만들지 여부를 지정합니다.  
  
 **대상 테이블/파일의 행 삭제**  
 새 데이터를 로드하기 전에 기존 테이블에서 데이터를 지울지 여부를 지정합니다.  
  
 **대상 테이블/파일에 행 추가**  
 기존 테이블에 이미 있는 데이터에 새 데이터를 추가할지 여부를 지정합니다.  
  
 **SQL 편집**  
 기본 문을 사용 합니다 **테이블 생성 SQL 문** 대화 상자 또는 용도 맞게 수정 합니다. 이 문을 수정하는 경우 테이블 매핑에서도 관련 내용을 변경해야 합니다.  
  
 **대상 테이블을 삭제하고 다시 만들기**  
 대상 테이블을 덮어쓰려면 이 옵션을 선택합니다. 이 옵션은 마법사를 사용하여 대상 테이블을 만들 때만 사용할 수 있습니다. 마법사에서 만든 패키지를 저장한 다음 해당 패키지를 다시 실행하는 경우에만 대상 테이블이 삭제되고 다시 생성됩니다.  
  
 **ID 삽입 가능**  
 원본 데이터의 기존 ID 값을 대상 테이블의 ID 열에 삽입할 수 있게 하려면 이 옵션을 선택합니다. 기본적으로 대상 ID 열에는 이러한 작업을 수행할 수 없습니다.  
  
 **매핑**  
 데이터 원본의 각 열이 대상의 열에 매핑되는 방식을 표시합니다.  
  
 이 목록에는 다음 열이 있습니다.  
  
 **원본**  
 변환 매개 변수를 설정할 수 있는 각 원본 열을 봅니다.  
  
 **대상**  
 복사 작업 중에 특정 열을 무시할지 여부를 지정합니다. 선택 하 여 열의 하위 집합만 복사할 수 있습니다  **\<무시 >** 건너 뛰 려는 열에 대해이 열에 있습니다. 열을 매핑하기 전에 매핑하지 않을 열은 모두 무시해야 합니다.  
  
 **형식**  
 열에 대한 데이터 형식을 선택합니다.  
  
 **Null 허용**  
 열에 Null 값을 허용할지 여부를 지정합니다.  
  
 **크기**  
 열의 문자 수를 지정합니다.  
  
 **정밀도**  
 표시된 데이터의 전체 자릿수(숫자의 자릿수)를 지정합니다.  
  
 **소수 자릿수**  
 표시된 데이터의 소수 자릿수(소수점 이하 자릿수)를 지정합니다.  
  
  
