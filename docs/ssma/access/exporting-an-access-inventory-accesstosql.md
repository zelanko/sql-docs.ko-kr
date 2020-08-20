---
description: 액세스 인벤토리 내보내기 (AccessToSQL)
title: 액세스 인벤토리 내보내기 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 112452e9e6c31810dbf26d9aa1e7b36959c192d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488336"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>액세스 인벤토리 내보내기 (AccessToSQL)
여러 Access 데이터베이스를 사용 하 고 마이그레이션할 데이터베이스를 모를 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트에 있는 모든 access 데이터베이스의 인벤토리를 내보낼 수 있습니다. 그런 다음 해당 데이터베이스 내에서 마이그레이션할 데이터베이스와 개체를 확인 하는 인벤토리 메타 데이터를 검토 하 고 쿼리할 수 있습니다. 이 인벤토리를 사용 하면 다음과 같은 질문에 대 한 답변을 신속 하 게 찾을 수 있습니다.  
  
-   가장 큰 데이터베이스는 무엇 인가요?  
  
-   누가 대부분의 데이터베이스를 소유 하 고 있나요?  
  
-   동일한 테이블이 포함 된 데이터베이스  
  
-   지난 6 개월 동안 수정 되지 않은 데이터베이스는 무엇입니까?  
  
-   개인 정보를 포함 하는 데이터베이스  
  
이러한 질문에 대답 하는 데 사용 되는 쿼리 예제는이 항목의 끝에 제공 됩니다.  
  
## <a name="exported-metadata"></a>내보낸 메타 데이터  
SSMA는 Access 데이터베이스, 테이블, 열, 인덱스, 외래 키, 쿼리, 보고서, 폼, 매크로 및 모듈에 대 한 메타 데이터를 내보냅니다. 이러한 항목의 각 범주에 대 한 메타 데이터를 별도 테이블로 내보냅니다. 이러한 테이블의 스키마는 [액세스 인벤토리 스키마](access-inventory-schemas-accesstosql.md)를 참조 하세요.  
  
## <a name="exporting-inventory-data"></a>인벤토리 데이터 내보내기  
액세스 인벤토리를 내보내려면 먼저 SSMA 프로젝트를 열거나 만든 다음 분석할 Access 데이터베이스를 추가 해야 합니다. SSMA 프로젝트에 데이터베이스를 추가한 후에는 해당 데이터베이스에 대 한 메타 데이터를 지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마로 내보냅니다. 필요한 경우 SSMA는 메타 데이터를 저장할 테이블을 만듭니다. 그런 다음 SSMA는 데이터베이스에 대 한 액세스 데이터베이스에 대 한 메타 데이터를 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
> Access 데이터베이스는 여러 파일로 분할 될 수 있습니다. 즉, 테이블을 포함 하는 백 엔드 데이터베이스와 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기가 포함 된 프런트 엔드 데이터베이스가 포함 됩니다. 분할 데이터베이스를로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프런트 엔드 데이터베이스를 SSMA에 추가 합니다.  
  
다음 지침에서는 프로젝트를 만들고, 프로젝트에 데이터베이스를 추가 하 고, 연결 하 여 인벤토리 데이터를 내보내는 방법에 대해 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**프로젝트를 만들려면**  
  
1.  Access 용 SSMA를 엽니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **이름** 입력란에 프로젝트 이름을  
  
4.  **위치** 상자에서 프로젝트에 대 한 폴더를 입력 하거나 선택 합니다.  
  
5.  다음 **으로 마이그레이션** 상자에서 마이그레이션할 대상 버전을 선택 하 고 **확인**을 클릭 합니다.  
  
프로젝트를 만드는 방법에 대 한 자세한 내용은 [프로젝트 만들기 및 관리](creating-and-managing-projects-accesstosql.md)를 참조 하세요.  
  
**데이터베이스를 찾아서 추가 하려면**  
  
1.  **파일** 메뉴에서 **데이터베이스 찾기**를 클릭 합니다.  
  
2.  데이터베이스 찾기 마법사에서 검색 하려는 드라이브, 파일 경로 또는 UNC 경로를 입력 합니다. 또는 **찾아보기** 를 클릭 하 여 드라이브 또는 네트워크 폴더를 선택 합니다.  
  
3.  **추가** 를 클릭 하 여 위치를 목록 상자에 추가 합니다.  
  
    이전 두 단계를 반복 하 여 추가 검색 위치를 추가 합니다.  
  
4.  필요에 따라 검색 조건을 추가 하 여 반환 되는 데이터베이스 목록을 구체화 합니다.  
  
    > [!IMPORTANT]  
    > **파일 이름 텍스트 상자의 전체 또는 일부** 는 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  **검색**을 클릭 합니다.  
  
    검색 페이지가 나타납니다. 찾은 데이터베이스와 검색 진행률이 표시 됩니다. 검색을 중지 하려면 **중지**를 클릭 합니다.  
  
6.  파일 선택 페이지에서 프로젝트에 추가 하려는 각 데이터베이스를 선택 합니다.  
  
    목록의 맨 위에 있는 **모두 선택** 및 **모두 지우기** 단추를 사용 하 여 모든 데이터베이스를 선택 하거나 선택 취소할 수 있습니다. CTRL 키를 누른 채 여러 행을 선택 하거나 SHIFT 키를 누른 채 행 범위를 선택할 수도 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 **마침**을 클릭 합니다.  
  
프로젝트에 데이터베이스를 추가 하는 방법에 대 한 자세한 내용은 [Access 데이터베이스 파일 추가 및 제거](adding-and-removing-access-database-files-accesstosql.md)를 참조 하세요.  
  
**SQL Server에 연결하려면**  
  
1.  **파일** 메뉴에서 **SQL Server에 연결**을 선택 합니다.  
  
2.  연결 대화 상자에서 인스턴스의 이름을 입력 하거나 선택 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 **localhost** 또는 점 (**.**)을 입력할 수 있습니다.  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.  
  
    -   명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 입력 합니다. 예: MyServer\MyInstance.  
  
3.  **데이터베이스** 상자에 내보낸 메타 데이터에 대 한 대상 데이터베이스의 이름을 입력 합니다.  
  
4.  인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서버 포트** 상자에서 연결에 사용 되는 포트 번호를 입력 합니다. 기본 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA는 Browser 서비스에서 포트 번호를 가져오려고 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
5.  **인증** 드롭다운 메뉴에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 **Windows 인증**을 선택 합니다. 로그인을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server 인증**을 선택 하 고 사용자 이름 및 암호를 제공 합니다.  
  
에 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server &#40;AccessToSQL&#41;에 연결 ](../../ssma/access/connecting-to-sql-server-accesstosql.md)을 참조 하세요.  
  
**인벤토리 정보를 내보내려면**  
  
1.  액세스 메타 데이터 탐색기에서 **access-메타 베이스**를 확장 합니다.  
  
2.  **데이터베이스**옆의 확인란을 선택 합니다.  
  
    개별 데이터베이스 또는 데이터베이스 개체를 생략 하려면 데이터베이스 폴더를 확장 한 다음 데이터베이스 또는 데이터베이스 개체 옆에 있는 확인란의 선택을 **취소 합니다.**  
  
3.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **스키마 내보내기**를 선택 합니다.  
  
4.  **내보내기에 대 한 스키마 선택** 대화 상자에서 내보낸 메타 데이터에 대 한 대상 스키마를 선택한 다음 **확인**을 클릭 합니다.  
  
메타 데이터를 내보낼 때마다 SSMA는 인벤토리에 데이터를 추가 합니다. 인벤토리에 있는 기존 데이터는 업데이트 되거나 삭제 되지 않습니다.  
  
## <a name="querying-the-exported-metadata"></a>내보낸 메타 데이터 쿼리  
액세스 데이터베이스에 대 한 메타 데이터를 내보낸 후 메타 데이터를 쿼리할 수 있습니다. 다음 지침에서는의 쿼리 편집기 창을 사용 하 여 쿼리를 실행 하는 방법을 설명 합니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
**메타 데이터를 쿼리하려면**  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** 또는 microsoft ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008** 또는 **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**을 차례로 가리킨 다음 **SQL Server Management Studio**을 클릭 합니다.  
  
2.  **서버에 연결** 대화 상자에서 설정을 확인 한 다음 **연결**을 클릭 합니다.  
  
3.  Management Studio 도구 모음에서 **새 쿼리** 를 클릭 하 여 쿼리 편집기를 엽니다.  
  
4.  쿼리 편집기 창에서 쿼리를 입력 합니다. 다음 섹션에서는 몇 가지 예를 보여 줍니다.  
  
5.  F5 키를 눌러 쿼리를 실행 합니다.  
  
## <a name="query-examples"></a>쿼리 예제  
다음 쿼리를 실행 하기 전에 *database_name* 쿼리를 실행 하 여 내보낸 메타 데이터가 포함 된 데이터베이스에 대해 쿼리가 실행 되 고 있는지 확인 해야 합니다. 예를 들어 메타 데이터를 MyAccessMetadata 라는 데이터베이스로 내보낸 경우 코드의 시작 부분에 다음을 추가 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
```  
USE MyAccessMetadata;  
GO  
```  
다음 예에서는 모두 **dbo** 스키마를 사용 합니다. 메타 데이터를 다른 스키마로 내보낸 경우 이러한 쿼리를 실행할 때 스키마를 변경 해야 합니다.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>이러한 데이터베이스에 있는 테이블 및 열은 무엇 인가요?  
다음 쿼리는 열, 테이블 및 데이터베이스 메타 데이터가 포함 된 테이블을 조인한 다음 열 이름을 기준으로 정렬 된 모든 데이터베이스, 테이블 및 열의 이름을 반환 합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>가장 큰 데이터베이스는 무엇 인가요?  
다음 쿼리는 각 Access 데이터베이스의 데이터베이스 이름, 파일 크기 및 테이블 수를 파일 크기 별로 정렬 하 여 반환 합니다.  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>대부분의 데이터베이스 소유자는 누구 인가요?  
다음 쿼리는 각 Access 데이터베이스의 소유자를 기준으로 정렬 된 데이터베이스 이름 및 소유자를 반환 합니다.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>동일한 테이블이 포함 된 데이터베이스  
다음 쿼리에서는 하위 쿼리를 사용 하 여 테이블 목록에 두 번 이상 나타나는 테이블 이름을 모두 찾은 다음 테이블 목록을 사용 하 여 데이터베이스 이름을 가져옵니다. 결과는 데이터베이스 이름으로 반환 된 다음 테이블 이름으로 반환 되 고 테이블 이름을 기준으로 정렬 됩니다.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>지난 6 개월 동안 수정 되지 않은 데이터베이스는 무엇입니까?  
다음 쿼리는 현재 날짜를 가져오고 6 개월 전에 월 값을 가져온 다음 수정 된 날짜가 6 개월 이전인 데이터베이스 목록을 반환 합니다.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>개인 정보를 포함 하는 데이터베이스  
액세스 데이터베이스에는 중요 한 정보나 개인 정보가 포함 될 수 있습니다. 이러한 데이터베이스를로 이동 하 여 보안 기능을 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 중요 한 데이터를 포함 하는 열에 특정 이름이 있거나 특정 문자를 포함 하는 경우 쿼리를 사용 하 여 해당 정보가 포함 된 모든 열을 찾을 수 있습니다. 예를 들어 "salary" 문자열이 포함 된 모든 열을 찾을 수 있습니다.  그런 다음 쿼리는 데이터베이스 이름, 테이블 이름 및 열 이름을 반환 합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
열 이름을 모르는 경우 모든 열을 반환 하는 쿼리를 작성할 수 있습니다. 이렇게 하려면 이전 쿼리에서 WHERE 절을 제거 합니다.  
  
## <a name="see-also"></a>관련 항목  
[마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)  
  
