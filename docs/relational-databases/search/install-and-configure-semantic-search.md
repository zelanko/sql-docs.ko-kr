---
title: 의미 체계 검색 설치 및 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6816d53fb9b9c8bc79bec05623640c91f9edd3d8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="install-and-configure-semantic-search"></a>의미 체계 검색 설치 및 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  통계 의미 체계 검색을 위한 필수 구성 요소와 이러한 필수 구성 요소의 설치 또는 확인 방법에 대해 설명합니다.  
  
## <a name="install-semantic-search"></a>의미 체계 검색 설치  
  
###  <a name="HowToCheckInstalled"></a> 의미 체계 검색이 설치되어 있는지 확인  
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) 메타데이터 함수의 **IsFullTextInstalled** 속성을 쿼리합니다.  
  
 반환 값이 1이면 전체 텍스트 검색과 의미 체계 검색이 설치되어 있음을 나타내고, 반환 값이 0이면 그렇지 않음을 나타냅니다.  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a> 의미 체계 검색 설치  
 의미 체계 검색을 설치하려면 SQL Server 설치 중에 **설치할 기능** 페이지에서 **검색을 위한 전체 텍스트 및 의미 체계 추출**을 선택합니다.  
  
 통계 의미 체계 검색은 전체 텍스트 검색을 기반으로 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이 두 가지 선택적 기능이 함께 설치됩니다.  
  
## <a name="install-the-semantic-language-statistics-database"></a>의미 체계 언어 통계 데이터베이스 설치  
 의미 체계 검색에는 의미 체계 언어 통계 데이터베이스라고 하는 추가적인 외부 종속성이 있습니다. 이 데이터베이스는 의미 체계 검색에 필요한 통계적 언어 모델을 포함합니다. 단일 의미 체계 언어 통계 데이터베이스에는 의미 체계 인덱싱에 지원되는 모든 언어에 대한 언어 모델이 포함되어 있습니다.  
  
###  <a name="HowToCheckDatabase"></a> 의미 체계 언어 통계 데이터베이스가 설치되어 있는지 확인  
 카탈로그 뷰 [sys.fulltext_semantic_language_statistics_database&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)를 쿼리합니다.  
  
 인스턴스에 대해 의미 체계 언어 통계 데이터베이스를 설치하여 등록한 경우 쿼리 결과에 데이터베이스에 대한 단일 정보 행이 포함되어 있습니다.  
  
```sql  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a> 의미 체계 언어 통계 데이터베이스 설치, 연결 및 등록  
 의미 체계 언어 통계 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 통해 설치되지 않습니다. 의미 체계 언어 통계 데이터베이스를 의미 체계 인덱싱을 위한 필수 구성 요소로 설정하려면 다음을 수행합니다.  
  
 **1. 의미 체계 언어 통계 데이터베이스를 설치합니다.**  
 
 1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에서 의미 체계 언어 통계 데이터베이스를 찾거나 웹에서 다운로드합니다.  
  
        1.  **설치 미디어에서** SemanticLanguageDatabase.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라는 Windows Installer 패키지를 찾습니다.  
  
        2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 다운로드 센터의 [Microsoft® SQL Server® 2016 의미 체계 언어 통계](https://www.microsoft.com/en-us/download/details.aspx?id=52681) 페이지에서 설치 관리자 패키지를 다운로드합니다.  
  
2.  **SemanticLanguageDatabase.msi** Windows Installer 패키지를 실행하여 데이터베이스 및 로그 파일을 추출합니다.  
  
     필요에 따라 대상 디렉터리를 변경할 수 있습니다. 기본적으로 설치 관리자는 Program Files 폴더의 **Microsoft Semantic Language Database** 폴더에 파일을 추출합니다. MSI 파일에는 압축된 데이터베이스 파일 및 로그 파일이 포함되어 있습니다.  
  
3.  추출한 데이터베이스 파일 및 로그 파일을 파일 시스템의 적절한 위치로 이동합니다.  
  
     이러한 파일을 기본 위치에 그대로 둘 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스를 위해 또 다른 데이터베이스 복사본을 추출할 수 없습니다.  
  
    > [!IMPORTANT]  
    >  의미 체계 언어 통계 데이터베이스를 추출할 때 파일 시스템의 기본 위치에 있는 데이터베이스 파일 및 로그 파일에 제한된 사용 권한이 할당됩니다. 따라서 이 파일을 기본 위치에 그대로 둘 경우 데이터베이스에 연결할 수 있는 권한이 없을 수 있습니다. 데이터베이스를 연결하려고 할 때 오류가 발생하는 경우 파일을 이동하거나 파일 시스템 사용 권한이 적절한지 확인하여 수정하세요.  
  
 **2. 의미 체계 언어 통계 데이터베이스를 연결합니다.**
   
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하거나 **FOR ATTACH** 구문으로 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 호출하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스를 연결합니다. 자세한 내용은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하세요.  
  
 기본적으로 데이터베이스의 이름은 **semanticsdb**입니다. 필요에 따라 데이터베이스를 연결할 때 데이터베이스에 다른 이름을 지정할 수 있습니다. 이후 단계에서 데이터베이스를 등록할 때 이 이름을 제공해야 합니다.  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 이 코드 예제에서는 데이터베이스를 기본 위치에서 새 위치로 이동했다고 가정합니다.  
  
 **3. 의미 체계 언어 통계 데이터베이스를 등록합니다.** 
  
 저장 프로시저 [sp_fulltext_semantic_register_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)를 호출하고 연결 시 데이터베이스에 지정한 이름을 제공합니다.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  

##  <a name="reqinstall"></a> 의미 체계 언어 통계 데이터베이스에 대한 요구 사항 및 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스별로 하나의 의미 체계 언어 통계 데이터베이스만 연결하고 등록할 수 있습니다.  
  
     단일 컴퓨터의 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스마다 의미 체계 언어 통계 데이터베이스의 물리적 복사본이 하나씩 필요합니다. 인스턴스마다 하나의 복사본을 연결합니다.  
  
-   등록된 올바른 의미 체계 언어 통계 데이터베이스를 분리하고 이름이 동일한 임의의 데이터베이스로 바꿀 수 없습니다. 이렇게 하면 활성 또는 이후 인덱스 채우기가 실패할 수 있습니다.  
  
-   의미 체계 언어 통계 데이터베이스는 읽기 전용입니다. 이 데이터베이스를 사용자 지정할 수는 없습니다. 어떤 식으로든 데이터베이스의 내용을 변경하면 이후 의미 체계 인덱싱의 결과는 신뢰할 수 없게 됩니다. 이 데이터의 원래 상태로 복원하려면 변경된 데이터베이스를 삭제하고 데이터베이스의 변경되지 않은 새 복사본을 다운로드하여 연결하면 됩니다.  
  
-   의미 체계 언어 통계 데이터베이스를 분리하거나 삭제할 수 있습니다. 데이터베이스에 대해 읽기 잠금을 설정하고 있는 활성 인덱싱 작업이 있는 경우에는 분리 또는 삭제 작업이 실패하거나 시간 초과됩니다. 이는 기존 동작과 일치합니다. 데이터베이스를 제거하면 의미 체계 인덱싱 작업이 실패합니다.  
 
##  <a name="HowToUnregister"></a> 의미 체계 언어 통계 데이터베이스 제거  

###  <a name="unregister-detach-and-remove-the-semantic-language-statistics-database"></a>의미 체계 언어 통계 데이터베이스 등록 취소, 분리 및 제거 

 **1. 의미 체계 언어 통계 데이터베이스 등록합니다.**
   
 저장 프로시저 [sp_fulltext_semantic_unregister_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)를 호출합니다. 인스턴스는 의미 체계 언어 통계 데이터베이스를 하나만 가질 수 있으므로 데이터베이스의 이름을 제공할 필요는 없습니다.  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **2. 의미 체계 언어 통계 데이터베이스를 분리합니다.**  
 
 저장 프로시저 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)를 호출하고 데이터베이스의 이름을 지정합니다.  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **3. 의미 체계 언어 통계 데이터베이스를 제거합니다.**  
 
 데이터베이스를 등록 취소하고 분리한 후 데이터베이스 파일을 간단히 삭제할 수 있습니다. 제거 프로그램은 없으며 제어판의 **프로그램 및 기능** 에도 해당 항목이 없습니다.  
  
## <a name="install-optional-support-for-newer-document-types"></a>최신 문서 유형에 대한 선택적 지원 설치  
  
###  <a name="office"></a> Microsoft Office 및 다른 Microsoft 문서 유형에 대한 최신 필터 설치  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서는 최신 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 단어 분리기 및 형태소 분석기를 설치하지만 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 문서 및 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 문서 유형용 최신 필터는 설치하지 않습니다. 이 필터는 최신 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 및 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 응용 프로그램을 사용하여 만든 문서를 인덱싱하는 데 필요합니다. 최신 필터를 다운로드하려면 [Microsoft Office 2010 Filter Packs](http://go.microsoft.com/fwlink/?LinkId=218293)를 참조하세요. (Office 2013 또는 Office 2016의 경우 Filter Pack 릴리스가 표시되지 않습니다.)
  
  
