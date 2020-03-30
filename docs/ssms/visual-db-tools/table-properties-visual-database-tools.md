---
title: 테이블 속성
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: b53bed28d05d490b9b6d603260917f7ffbb4d047
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242178"
---
# <a name="table-properties-visual-database-tools"></a>테이블 속성(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
테이블 디자이너 내부를 마우스 오른쪽 단추로 클릭한 다음 속성을 선택하는 경우 속성 창에 이러한 속성이 나타납니다. 별도로 언급하지 않는 한 테이블을 선택할 때 속성 창에서 이러한 속성을 편집할 수 있습니다.  
  
> [!NOTE]  
> 테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.  
  
## <a name="show-table-properties-in-table-designer"></a>테이블 디자이너에서 테이블 속성 표시  
  
> [!NOTE]  
> 이 항목의 속성은 사전순 대신 범주별로 정렬됩니다.  
  
**ID 범주**  
확장하면 **이름**, **설명**및 **스키마**에 대한 속성이 표시됩니다.  
  
**이름**  
테이블의 이름을 표시합니다. 이름을 편집하려면 입력란에 입력합니다.  
  
> [!CAUTION]  
> 기존의 쿼리, 뷰, 사용자 정의 함수, 저장 프로시저 또는 프로그램에서 해당 테이블을 참조하는 경우 테이블의 이름을 수정하면 이 개체들은 유효하지 않게 됩니다.  
  
**데이터베이스 이름**  
선택한 테이블의 데이터 원본 이름을 표시합니다.  
  
**설명**  
선택한 테이블에 대한 설명을 표시합니다. 전체 설명을 보거나 편집하려면 설명을 클릭한 다음, 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다.  
  
**스키마**  
현재 테이블이 속해 있는 스키마의 이름을 표시합니다. Microsoft SQL Server에만 적용됩니다.  
  
**서버 이름**  
데이터 원본의 서버 이름을 표시합니다.  
  
**테이블 디자이너 범주**  
확장하면 **ID 열**, **인덱싱 가능**및 **복제됨**에 대한 속성이 표시됩니다.  
  
**ID 열**  
테이블의 ID 열로 사용되는 열을 표시합니다. ID 열을 변경하려면 드롭다운 목록에서 원하는 열을 선택합니다. 이 목록에는 숫자 데이터 형식의 열만 표시됩니다.  
  
**인덱싱 가능**  
테이블을 인덱싱할 수 있는지 여부를 표시합니다. 테이블을 인덱싱할 수 없는 경우 테이블 소유자가 아니거나 데이터 형식이 텍스트, ntext 또는 이미지인 열이 테이블에 포함되어 있기 때문일 수 있습니다.  
  
**복제됨**  
테이블이 다른 위치에 복제되었는지 여부를 나타냅니다.  
  
**기본 데이터 공간 사양 범주**  
확장하면 **(데이터 공간 형식)** , **파일 그룹 또는 파티션 구성표 이름**및 **파티션 열 목록**에 대한 속성이 표시됩니다.  
  
**(데이터 공간 형식)**  
현재 테이블을 저장하는 데 파일 그룹을 사용했는지 분할 구성표를 사용했는지 여부를 표시합니다.  
  
**파일 그룹 또는 파티션 구성표 이름**  
파일 그룹 또는 분할 구성표의 이름을 표시합니다.  
  
**파티션 열 목록**  
**파티션 열 목록** 대화 상자에 액세스할 수 있습니다.  
  
**행 GUID 열**  
Microsoft SQL Server에서 테이블의 ROWGUID 열로 사용되는 열을 표시합니다. ROWGUID 열을 변경하려면 드롭다운 목록에서 원하는 열을 선택합니다. SQL Server 7.0 이상에만 적용됩니다.  
  
**Text/Image 파일 그룹**  
데이터 형식이 텍스트 또는 이미지인 열에 대한 파일 그룹을 선택하는 데 사용할 수 있는 드롭다운 목록을 제공합니다. 분할 구성표를 사용하여 테이블을 저장한 경우 이 필드를 비워 둡니다.  
  
## <a name="see-also"></a>참고 항목  
[테이블 디자인](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
