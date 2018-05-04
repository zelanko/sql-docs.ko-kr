---
title: 액세스 인벤토리 (AccessToSQL) 내보내기 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 32029fcc4e3af80cf0c3600468b6209e1241dc94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="exporting-an-access-inventory-accesstosql"></a>액세스 인벤토리 (AccessToSQL) 내보내기
Access 데이터베이스를 여러 개 있고로 마이그레이션할 수 있는 대상을 확실 하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 프로젝트에서 모든 Access 데이터베이스의 인벤토리를 내보낼 수 있습니다. 그런 다음 검토 및 쿼리할 수 있습니다 인벤토리 메타 데이터를 마이그레이션하려면 해당 데이터베이스 내의 개체 및 데이터베이스를 결정 합니다. 이 인벤토리 하면 신속 하 게 다음과 같은 질문에 답변 찾기:  
  
-   큰 데이터베이스의 경우은 무엇입니까?  
  
-   대부분의 데이터베이스 소유자는 누구?  
  
-   데이터베이스를 같은 테이블에 포함?  
  
-   데이터베이스를 지난 6 개월 동안에서 수정 되지 않은?  
  
-   데이터베이스에 개인 정보가 있습니까?  
  
이러한 질문에 대답 하는 데 사용 되는 쿼리 예제는이 항목의 끝에서 제공 됩니다.  
  
## <a name="exported-metadata"></a>내보낸된 메타 데이터  
SSMA는 Access 데이터베이스, 테이블, 열, 인덱스, 외래 키, 쿼리, 보고서, 폼, 매크로 및 모듈에 대 한 메타 데이터를 내보냅니다. 이러한 각 범주 항목에 대 한 메타 데이터를 별도 테이블에 내보내집니다. 이러한 테이블의 스키마에 대 한 참조 [액세스 인벤토리 스키마](http://msdn.microsoft.com/en-us/fdd3cff2-4d62-4395-8acf-71ea8f17f524)합니다.  
  
## <a name="exporting-inventory-data"></a>인벤토리 데이터 내보내기  
액세스 인벤토리를 내보내려면 먼저 열 또는 SSMA 프로젝트를 만들 하며 분석 하려면 Access 데이터베이스를 추가 합니다. 지정 된 해당 데이터베이스에 대 한 메타 데이터를 내보낼 데이터베이스 SSMA 프로젝트에 추가한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 및 스키마입니다. 필요한 경우 SSMA 메타 데이터를 저장 하는 테이블을 만듭니다. SSMA는 Access 데이터베이스에 대 한 메타 데이터를 추가 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
> [!NOTE]  
> Access 데이터베이스를 여러 파일로 분할할 수 있습니다: 테이블 및 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기 키를 포함 하는 프런트 엔드 데이터베이스를 포함 하는 백 엔드 데이터베이스입니다. 데이터베이스를 분할 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 프런트 엔드 데이터베이스 SSMA를 추가 합니다.  
  
다음 지침에는 프로젝트 만들기, 프로젝트에 데이터베이스를 추가에 연결 하는 방법을 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 다음 인벤토리 데이터를 내보냅니다.  
  
**프로젝트를 만들려면**  
  
1.  Access 용 SSMA를 엽니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **이름** 입력란에 프로젝트 이름을  
  
4.  에 **위치** 입력란에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
5.  에 **마이그레이션 대상** 콤보 상자에서 다음을 클릭 하 고 마이그레이션하려 대상 버전 선택 **확인**합니다.  
  
프로젝트를 만드는 방법에 대 한 자세한 내용은 참조 [만들기 및 프로젝트 관리](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)합니다.  
  
**찾아 데이터베이스를 추가 합니다.**  
  
1.  에 **파일** 메뉴를 클릭 하 여 **찾을 데이터베이스**합니다.  
  
2.  데이터베이스 검색 마법사에는 드라이브, 파일 경로 또는 검색할 UNC 경로 입력 합니다. 또는 클릭 하 여 **찾아보기** 드라이브 또는 네트워크 폴더를 선택 합니다.  
  
3.  클릭 **추가** 목록 상자에 위치를 추가 합니다.  
  
    추가 검색 위치를 추가 하려면 이전 두 단계를 반복 합니다.  
  
4.  필요에 따라 반환 되는 데이터베이스의 목록을 구체화 하려면 검색 조건을 추가 합니다.  
  
    > [!IMPORTANT]  
    > **전체 또는 일부 파일 이름의** 입력란 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  클릭 **스캔**합니다.  
  
    검색 페이지가 표시 됩니다. 여기에 발견 된 데이터베이스 및 검색 진행률 표시. 검색을 중지 하려면 클릭 **중지**합니다.  
  
6.  파일 선택 페이지에서 프로젝트에 추가 하려는 각 데이터베이스를 선택 합니다.  
  
    사용할 수는 **모두 선택** 및 **모두 지우기** 선택 하거나 모든 데이터베이스를 선택 취소 하는 목록의 위쪽에 있는 단추입니다. 여러 행을 선택 하려면 CTRL 키를 누른 채로 또는 SHIFT 키를 선택 하는 행 범위 아래로 수도 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 클릭 **마침**합니다.  
  
데이터베이스 프로젝트에 추가 하는 방법에 대 한 자세한 내용은 참조 [Access 데이터베이스 파일을 제거 및 추가](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)합니다.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Server에 연결**합니다.  
  
2.  연결 대화 상자에서 이름을 입력 하거나 선택 된 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있는 **localhost** 또는 점 (**.**).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 입력 합니다. 예를 들어: MyServer\MyInstance 합니다.  
  
3.  에 **데이터베이스** 상자 내보낸된 메타 데이터에 대 한 대상 데이터베이스의 이름을 입력 합니다.  
  
4.  경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 사용 되는 포트 번호를 입력, 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 연결 모드는 **서버 포트** 상자입니다. 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 기본 포트 번호는 1433입니다. 명명 된 인스턴스에 대 한 SSMA에서 포트 번호 가져오기를 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 서비스입니다.  
  
5.  에 **인증** 드롭 다운 메뉴에서 선택 된 연결에 사용할 인증 유형을 합니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인을 **SQL Server 인증**, 사용자 이름 및 암호를 제공 합니다.  
  
에 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [SQL Server에 연결 &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)합니다.  
  
**인벤토리 정보를 내보내려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스 메타 베이스**합니다.  
  
2.  옆에 확인란을 선택 **데이터베이스**합니다.  
  
    개별 데이터베이스 또는 데이터베이스 개체를 생략 하려면 확장 된 **데이터베이스** 폴더 및 데이터베이스 또는 데이터베이스 개체 옆의 확인란 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스** 선택 **스키마 내보내기**합니다.  
  
4.  에 **내보내기에 대 한 스키마 선택** 대화 상자에서 내보낸된 메타 데이터에 대 한 대상 스키마를 선택 하 고 클릭 **확인**합니다.  
  
메타 데이터를 내보낼 때마다 SSMA 인벤토리 데이터를 추가 합니다. 인벤토리의 기존 데이터를 업데이트 하거나 삭제 합니다.  
  
## <a name="querying-the-exported-metadata"></a>내보낸된 메타 데이터 쿼리  
Access 데이터베이스에 대 한 메타 데이터를 내보낸 후에 메타 데이터를 쿼리할 수 있습니다. 다음 지침에서 쿼리 편집기 창을 사용 하 여 설명 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 쿼리를 실행 합니다.  
  
**메타 데이터를 쿼리**  
  
1.  **시작** 메뉴에서 **모든 프로그램**, 가리킨 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005** 또는 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008** 또는 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012**, 클릭 하 고 **SQL Server Management Studio**합니다.  
  
2.  에 **서버에 연결** 대화 상자에서 설정을 확인 하 고 클릭 **연결**합니다.  
  
3.  Management Studio 도구 모음에서 **새 쿼리** 쿼리 편집기를 엽니다.  
  
4.  쿼리 편집기 창에서 쿼리를 입력 합니다. 몇 가지 예는 다음 섹션에 표시 됩니다.  
  
5.  쿼리를 실행 하려면 F5 키를 누릅니다.  
  
## <a name="query-examples"></a>쿼리 예제  
다음 쿼리를 실행 하기 전에 사용 하는 실행 해야 *database_name* 쿼리를 쿼리 내보낸된 메타 데이터를 포함 하는 데이터베이스에 대해 실행 되 고 있는지 확인 합니다. 예를 들어 MyAccessMetadata 라는 데이터베이스에 메타 데이터를 내보낸 경우 추가한 다음의 시작 부분에는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 코드:  
  
```  
USE MyAccessMetadata;  
GO  
```  
다음 예에서는 모두 사용 하 여는 **dbo** 스키마입니다. 다른 스키마에 메타 데이터를 내보낼 경우 이러한 쿼리를 실행 하는 경우 스키마를 변경 해야 합니다.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>테이블 및 열에는 이러한 데이터베이스에는 있습니까?  
다음 쿼리는 열, 테이블 및 데이터베이스 메타 데이터를 포함 하는 테이블을 조인 하 고의 모든 데이터베이스, 테이블 및 열 이름으로 정렬 하는 열 이름을 반환 합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>큰 데이터베이스의 경우은 무엇입니까?  
다음 쿼리에서 파일 크기 별로 정렬 된 각 Access 데이터베이스의 데이터베이스 이름, 파일 크기 및 테이블의 수를 반환 합니다.  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>대부분의 데이터베이스 소유자가 누군지 않습니까?  
다음 쿼리는 데이터베이스 이름과 소유자에 의해 정렬 된 각 Access 데이터베이스의 소유자를 반환 합니다.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>데이터베이스를 같은 테이블에 포함?  
다음 쿼리에서 하위 쿼리를 사용 하 여 테이블, 목록에 두 번 이상 나타나는 모든 테이블 이름을 찾을 수와 다음이 목록은 테이블을 사용 하 여 데이터베이스 이름을 가져오지 못했습니다. 결과는 데이터베이스 이름 및 테이블 이름으로 반환 되 고 테이블 이름으로 정렬 됩니다.  
  
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
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>데이터베이스를 지난 6 개월 동안에서 수정 되지 않은?  
다음 쿼리는 현재 날짜를 가져옵니다, 그리고 6 개월에 대 한 월 값을 가져옵니다 및 다음 6 개월 보다 큰의 수정 된 날짜를 사용 하 여 데이터베이스의 목록을 반환 합니다.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>데이터베이스에 개인 정보가 있습니까?  
Access 데이터베이스에는 중요 한 정보나 개인 정보가 포함 될 수 있습니다. 이러한 데이터베이스를 이동 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 해당 보안 기능을 활용할 수 있습니다. 중요 한 데이터가 포함 된 열 특정 이름을 가진 또는 특정 문자를 포함할를 알고 있는 경우 해당 정보를 포함 하는 모든 열을 찾으려면 쿼리를 사용할 수 있습니다. 예를 들어 "급여" 문자열이 포함 된 모든 열을 찾을 수 있습니다.  쿼리는 다음 데이터베이스 이름, 테이블 이름 및 열 이름을 반환합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
열 이름을 모르는 경우에 모든 열을 반환 하는 쿼리를 작성할 수 있습니다. 이 수행 하려면 이전 쿼리에서 WHERE 절을 제거 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[Access 데이터베이스 마이그레이션을 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
