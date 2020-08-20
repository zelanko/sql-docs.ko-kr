---
description: 테이블 생성 SQL 문(SQL Server 가져오기 및 내보내기 마법사)
title: 테이블 생성 SQL 문(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7854a8121c16d263da900ffc3f8475a4fe4dddff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484141"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>테이블 생성 SQL 문(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


**열 매핑** 대화 상자에서 **대상 테이블 만들기** 를 선택한 다음 **SQL 편집** 을 선택하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **테이블 생성 SQL 문** 대화 상자를 표시합니다. 이 페이지에서 마법사가 새 대상 테이블을 만들기 위해 실행하는 **CREATE TABLE** 명령을 검토하고 필요에 따라 사용자 지정합니다.
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사의 **테이블 생성 SQL 문** 대화 상자가 아니라 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE 문에 대한 정보를 찾으려는 경우 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>테이블 생성 SQL 문 페이지의 스크린샷  
 다음 스크린샷은 마법사의 **테이블 생성 SQL 문** 대화 상자를 보여 줍니다.
 
이 예제에서는 **SQL 문** 상자에 마법사에서 생성된 기본 **CREATE TABLE** 문이 포함되어 있습니다. 이 명령문은 **Person.Address** 원본 테이블의 복사본인 **Person.AddressNew**라는 대상 테이블을 만듭니다. 
  
 ![가져오기 및 내보내기 마법사의 테이블 만들기 페이지](../../integration-services/import-export-data/media/create-table.png "가져오기 및 내보내기 마법사의 테이블 만들기 페이지")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>CREATE TABLE 문 검토 또는 다시 생성  
 **SQL 문**  
자동으로 생성된 SQL 문을 표시하고 사용자 지정할 수 있게 합니다.
 
기본 CREATE TABLE 명령을 변경하는 경우 **열 매핑** 대화 상자로 돌아갈 때 관련 열 매핑을 변경해야 할 수도 있습니다.  
  
SQL 문의 텍스트에 캐리지 리턴을 포함하려면 Ctrl+Enter를 누릅니다. Enter 키만 누르면 대화 상자가 닫힙니다.  
  
CREATE TABLE 문과 구문에 대한 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.   
  
 **자동 생성**  
 기본 SQL 명령문을 수정한 경우 **자동 생성**을 클릭하여 복원합니다.  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>FILESTREAM 열을 포함하는 테이블 만들기  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 이 기본 CREATE TABLE 문은 원본 테이블에 FILESTREAM 열이 있는 경우에도 FILESTREAM 특성을 포함하지 않습니다.
 1.  마법사를 사용하여 FILESTREAM 열을 복사하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현합니다.
 2.  그런 다음 **테이블 생성 SQL 문** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 수동으로 추가합니다.  

구문에 대한 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. FILESTREAM에 대한 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
## <a name="whats-next"></a>다음 작업  
 CREATE TABLE 명령을 검토 및 사용자 지정하고 **확인**을 클릭하면 **테이블 생성 SQL 문** 대화 상자가 **열 매핑** 대화 상자로 돌아갑니다. 자세한 내용은 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.
 
 ## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


