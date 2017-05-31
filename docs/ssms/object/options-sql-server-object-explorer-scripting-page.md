---
title: "옵션(SQL Server 개체 탐색기 - 스크립팅 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d5353c0732833516e95cc734a2d7bbe0f1258554
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="options-sql-server-object-explorer---scripting-page"></a>옵션(SQL Server 개체 탐색기 - 스크립팅 페이지)
이 페이지를 사용하여 **개체 탐색기**의 개체 컨텍스트 메뉴에서 다음 명령에 적용되는 스크립팅 옵션을 설정할 수 있습니다.  
  
-   사용자 테이블 및 뷰에 대한 **편집** 명령  
  
-   사용자가 만든 개체에 대한 **<object> 스크립팅** 명령  
  
-   사용자가 만든 개체에 대한 **수정** 명령  
  
-   이 페이지에서는 **SQL Server 스크립트 생성 마법사**에 대한 스크립팅 옵션의 기본값도 설정합니다.  
  
## <a name="remarks"></a>주의  
**편집** 및 **수정** 명령은 동일한 옵션 설정에 대해 **<object> 스크립팅** 명령과 다른 결과를 생성할 수 있습니다. **편집** 및 **수정** 명령은 쿼리 편집기 세션 중에 현재 데이터베이스의 개체를 수정하기 위해 디자인되었고, **<object> 스크립팅** 명령은 나중에 개체를 만드는 데 사용할 수 있도록 스크립트를 생성하기 위해 디자인되었습니다.  
  
## <a name="options"></a>옵션  
각 옵션 오른쪽의 목록에 있는 사용 가능한 설정에서 선택하여 스크립팅 옵션을 지정합니다.  
  
### <a name="general-scripting-options"></a>일반 스크립팅 옵션  
**개별 문 구분**  
일괄 처리 구분 기호를 사용하여 개별 [!INCLUDE[tsql](../../includes/tsql_md.md)] 문을 구분합니다. **쿼리 편집기**에 대한 기본 일괄 처리 구분 기호를 변경하려면 **도구**/**옵션**/**쿼리 실행**/**SQL Server**/**일반**/**일괄 처리 구분 기호**를 선택합니다. 기본값은 False입니다. 자세한 내용은 [GO(Transact-SQL)](http://msdn.microsoft.com/en-us/b2ca6791-3a07-4209-ba8e-2248a92dd738)를 참조하세요.  
  
**설명 머리글 포함**  
스크립트를 개체별 섹션으로 구분하여 스크립트에 설명을 추가합니다. 기본값은 True입니다. 자세한 내용은 [/*...*/ (Comment)(Transact-SQL)](http://msdn.microsoft.com/en-us/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c)를 참조하세요.  
  
**VarDecimal 옵션 포함**  
VarDecimal 저장소 옵션을 포함합니다. 기본값은 False입니다. 자세한 내용은 [sp_db_vardecimal_storage_format(Transact-SQL)](http://msdn.microsoft.com/en-us/9920b2f7-b802-4003-913c-978c17ae4542)을 참조하세요.  
  
**변경 내용 추적 스크립팅**  
스크립트에 변경 내용 추적 정보를 포함합니다.  
  
**서버 버전에 대한 스크립트**  
선택한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 실행될 수 있는 스크립트를 만듭니다. [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 의 새 기능은 이전 버전에 대해 스크립팅될 수 없습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 에 대해 생성된 일부 스크립트는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]가 실행 중인 서버 또는 이전의 [데이터베이스 호환성 수준 설정](http://msdn.microsoft.com/en-us/ca5fd220-d5ea-4182-8950-55d4101a86f6)이 있는 데이터베이스에서 실행할 수 없습니다.  
  
**전체 텍스트 카탈로그 스크립팅**  
전체 텍스트 카탈로그에 대한 스크립트를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE FULLTEXT CATALOG(Transact-SQL)](http://msdn.microsoft.com/en-us/d7a8bd93-e2d7-4a40-82ef-39069e65523b)를 참조하세요.  
  
**USE 스크립팅 <database>**  
현재 **개체 탐색기** 데이터베이스의 컨텍스트에서 데이터베이스 개체를 만들기 위해 스크립트에 USE DATABASE 문을 추가합니다. 스크립트를 다른 데이터베이스에서 사용할 경우 False를 선택하여 생략합니다. 기본값은 True입니다. 자세한 내용은 [USE(Transact-SQL)](http://msdn.microsoft.com/en-us/c05acac8-c063-4770-8e36-d7f71d500b10)를 참조하세요.  
  
### <a name="object-scripting-options"></a>개체 스크립팅 옵션  
**종속 개체에 대해 스크립트 생성**  
선택한 개체에 대한 스크립트가 실행될 때 필요한 추가 개체에 대한 스크립트를 생성합니다. 기본값은 False입니다.  
  
**IF NOT EXISTS 절 포함**  
개체를 만들기 전에 데이터베이스에 해당 개체가 없는지 확인하는 문을 포함합니다. 기본값은 False입니다. 자세한 내용은 [IF...ELSE(Transact-SQL)](http://msdn.microsoft.com/en-us/676c881f-dee1-417a-bc51-55da62398e81) 및 [EXISTS(Transact-SQL)](http://msdn.microsoft.com/en-us/b6510a65-ac38-4296-a3d5-640db0c27631)를 참조하세요.  
  
**개체 이름 스키마 한정**  
개체 스키마로 개체 이름을 한정합니다. 기본값은 False입니다. 자세한 내용은 [데이터베이스 스키마 만들기](http://msdn.microsoft.com/en-us/ed2a5522-f4d2-4111-95a4-d3e1e5081739)를 참조하세요.  
  
**확장 속성 스크립팅**  
개체에 확장 속성이 있을 경우 스크립트에 확장 속성을 포함합니다. 기본값은 False입니다. 자세한 내용은 [sp_addextendedproperty(Transact-SQL)](http://msdn.microsoft.com/en-us/565483ea-875b-4133-b327-d0006d2d7b4c)를 참조하세요.  
  
**스크립트 소유자**  
생성된 스크립트에 소유자를 포함합니다. 기본값은 False입니다.  
  
**사용 권한 스크립팅**  
스크립트에 데이터베이스 개체에 대한 사용 권한을 포함합니다. 기본값은 True입니다. 자세한 내용은 [사용 권한](http://msdn.microsoft.com/en-us/f28e3dea-24e6-4a81-877b-02ec4c7e36b9)을 참조하세요.  
  
### <a name="tableview-options"></a>테이블/뷰 옵션  
다음 옵션은 테이블 또는 뷰에 대한 스크립트에만 적용됩니다.  
  
**사용자 정의 데이터 형식을 기본 유형으로 변환**  
사용자 정의 데이터 형식을 해당 유형 생성의 기반이 된 기본 유형으로 변환합니다. 원본 데이터베이스 사용자 정의 데이터 형식이 스크립트가 실행될 데이터베이스에 없으면 True를 사용합니다. 사용자 정의 데이터 형식을 유지하려면 False를 사용합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TYPE(Transact-SQL)](http://msdn.microsoft.com/en-us/2202236b-e09f-40a1-bbc7-b8cff7488905)을 참조하세요.  
  
**SET ANSI PADDING 명령 생성**  
각 CREATE TABLE 문의 앞뒤에 SET ANSI_PADDING 문을 추가합니다. 기본값은 True입니다. 자세한 내용은 [SET ANSI_PADDING(Transact-SQL)](http://msdn.microsoft.com/en-us/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0)을 참조하세요.  
  
**데이터 정렬 포함**  
열 정의에 데이터 정렬을 포함합니다. 기본값은 True입니다. 자세한 내용은 [Collation and Unicode Support](http://msdn.microsoft.com/en-us/92d34f48-fa2b-47c5-89d3-a4c39b0f39eb)을 참조하세요.  
  
**IDENTITY 속성 포함**  
IDENTITY 초기값 및 IDENTITY 증가값에 대한 정의를 포함합니다. 기본값은 True입니다. 자세한 내용은 [IDENTITY(속성)(Transact-SQL)](http://msdn.microsoft.com/en-us/8429134f-c821-4033-a07c-f782a48d501c)를 참조하세요.  
  
**외래 키 참조 스키마 한정**  
FOREIGN KEY 제약 조건에 대한 테이블 참조에 스키마 이름을 추가합니다. 기본값은 True입니다.  
  
**바인딩된 기본값 및 규칙 스크립팅**  
**sp_bindefault** 및 **sp_bindrule** 바인딩 저장 프로시저 호출을 포함합니다. 기본값은 True입니다. 자세한 내용은 [sp_bindefault(Transact-SQL)](http://msdn.microsoft.com/en-us/3da70c10-68d0-4c16-94a5-9e84c4a520f6) 및 [sp_bindrule(Transact-SQL)](http://msdn.microsoft.com/en-us/2606073e-c52f-498d-a923-5026b9d97e67)을 참조하세요.  
  
**CHECK 제약 조건 스크립팅**  
스크립트에 [CHECK 제약 조건](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e) 을 추가합니다. 기본값은 True입니다.  
  
**기본값 스크립팅**  
스크립트에 열 기본값을 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE DEFAULT(Transact-SQL)](http://msdn.microsoft.com/en-us/08475db4-7d90-486a-814c-01a99d783d41)를 참조하세요.  
  
**파일 그룹 스크립팅**  
테이블 정의에 대한 ON 절에 파일 그룹을 지정합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TABLE(Transact-SQL)](http://msdn.microsoft.com/en-us/1e068443-b9ea-486a-804f-ce7b6e048e8b)을 참조하세요.  
  
**외래 키 스크립팅**  
스크립트에 [FOREIGN KEY 제약 조건](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) 을 포함합니다. 기본값은 False입니다.  
  
**전체 텍스트 인덱스 스크립팅**  
스크립트에 전체 텍스트 인덱스를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE FULLTEXT INDEX(Transact-SQL)](http://msdn.microsoft.com/en-us/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)를 참조하세요.  
  
**인덱스 스크립팅**  
스크립트에 클러스터형, 비클러스터형 및 XML 인덱스를 포함합니다. 기본값은 True입니다. 자세한 내용은 [CREATE INDEX(Transact-SQL)](http://msdn.microsoft.com/en-us/d2297805-412b-47b5-aeeb-53388349a5b9)를 참조하세요.  
  
**파티션 구성표 스크립팅**  
스크립트에 테이블 파티션 구성표를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE PARTITION SCHEME(Transact-SQL)](http://msdn.microsoft.com/en-us/5b21c53a-b4f4-4988-89a2-801f512126e4)를 참조하세요.  
  
**기본 키 스크립팅**  
스크립트에 [PRIMARY KEY 및 FOREIGN KEY 제약 조건](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) 을 포함합니다. 기본값은 True입니다.  
  
**통계 스크립팅**  
스크립트에 사용자 정의 통계를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE STATISTICS(Transact-SQL)](http://msdn.microsoft.com/en-us/b23e2f6b-076c-4e6d-9281-764bdb616ad2)를 참조하세요.  
  
**트리거 스크립팅**  
스크립트에 트리거를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TRIGGER(Transact-SQL)](http://msdn.microsoft.com/en-us/edeced03-decd-44c3-8c74-2c02f801d3e7)를 참조하세요.  
  
**고유 키 스크립팅**  
스크립트에 [UNIQUE 제약 조건 및 CHECK 제약 조건](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e) 을 포함합니다. 기본값은 False입니다.  
  
**뷰 열 스크립팅**  
뷰 머리글에 뷰 열을 선언합니다. 기본값은 False입니다. 자세한 내용은 [CREATE VIEW(Transact-SQL)](http://msdn.microsoft.com/en-us/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9)를 참조하세요.  
  
**ScriptDriIncludeSystemNames**  
선언적 참조 무결성을 적용하기 위해 시스템 생성 제약 조건 이름을 포함합니다. 기본값은 False입니다. 자세한 내용은 [REFERENTIAL_CONSTRAINTS(Transact-SQL)](http://msdn.microsoft.com/en-us/5d358f18-0a85-4b55-af4b-98d5f4cd1020)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[스크립트 생성(SQL Server Management Studio)](http://msdn.microsoft.com/en-us/9711c617-3c68-4e5a-aea3-befc64d51524)  
  

