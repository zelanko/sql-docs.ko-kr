---
title: "데이터베이스 만들기(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa72ff1cc846db19f946bff714e97303c41306f3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>데이터베이스 만들기(SQL Server 가져오기 및 내보내기 마법사)
**대상 선택** 페이지에서 **새로 만들기** 를 선택하여 새 SQL Server 대상 데이터베이스를 만드는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에 **데이터베이스 만들기** 대화 상자가 표시됩니다. 이 페이지에서 새 데이터베이스의 이름을 입력합니다. 필요에 따라 새 데이터베이스의 처음 크기와 자동 증가 및 해당 로그 파일에 대한 설정을 변경할 수도 있습니다. 

마법사의 **데이터베이스 만들기** 대화 상자에는 새 SQL Server 데이터베이스를 만드는 데 사용할 수 있는 기본 옵션만 제공됩니다. 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 모든 옵션을 보고 구성하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스를 만들거나, 마법사가 생성한 후에 데이터베이스를 구성하세요. 

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사의 **데이터베이스 만들기** 대화 상자가 아니라 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE DATABASE 문에 대한 정보를 찾으려면 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  

## <a name="screen-shot-of-the-create-database-page"></a>데이터베이스 만들기 페이지의 스크린샷  
다음 스크린샷에서는 마법사의 **데이터베이스 만들기** 대화 상자를 보여 줍니다.  

![가져오기 및 내보내기 마법사의 데이터베이스 페이지 만들기](../../integration-services/import-export-data/media/create-database.png "가져오기 및 내보내기 마법사의 데이터베이스 페이지 만들기")  

## <a name="provide-a-name-for-the-new-database"></a>새 데이터베이스의 이름 입력  
**이름**  
 대상 SQL Server 데이터베이스의 이름을 제공합니다.
 
### <a name="naming-requirements"></a>명명 요구 사항
SQL Server 명명 규칙에 따라 데이터베이스의 이름을 지정해야 합니다.  
  
-   데이터베이스 이름은 SQL Server의 인스턴스 내에서 고유해야 합니다.  
  
-   데이터베이스 이름은 최대 123자까지 가능합니다. (SQL Server에서 데이터 파일 및 로그 파일에 추가하는 접미사에 5자를 허용하여 최대 128자 이내여야 합니다.)  
  
-   데이터베이스 이름은 SQL Server의 식별자에 대한 규칙을 준수해야 합니다. 다음은 가장 중요한 요구 사항입니다.  
  
    -   첫 문자는 문자, 밑줄(_), @ 기호 또는 숫자 기호(#)여야 합니다.  
  
    -   그다음 문자는 문자, 숫자, @ 기호, 달러 기호($), 숫자 기호 또는 밑줄이 될 수 있습니다.  
  
    -   공백이나 다른 특수 문자는 사용할 수 없습니다.  
  
이러한 요구 사항에 대한 자세한 내용은 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)를 참조하세요.  

## <a name="optionally-specify-data-file-and-log-file-options"></a>필요에 따라 데이터 파일 및 로그 파일 옵션 지정

> [!TIP]
> **이름** 필드에 새 데이터베이스의 이름을 제공해야 하지만 일반적으로 파일 크기 및 파일 증가에 대한 다른 설정은 기본값으로 유지할 수 있습니다.

### <a name="data-file-options"></a>데이터 파일 옵션  
 **처음 크기**  
 데이터 파일의 처음 크기(MB)를 지정합니다.  
  
 **증가 허용 안 함**  
 데이터 파일이 지정한 처음 크기 이상으로 증가할 수 있는지 여부를 지정합니다.  
  
 **백분율 단위로 증가**  
 데이터 파일의 증가 단위(백분율)를 지정합니다.  
  
 **크기 단위로 증가**  
 데이터 파일의 증가 단위(MB)를 지정합니다.  
  
### <a name="log-file-options"></a>로그 파일 옵션  
 **처음 크기**  
 로그 파일의 처음 크기(MB)를 지정합니다.  
  
 **증가 허용 안 함**  
 로그 파일이 지정한 처음 크기 이상으로 증가할 수 있는지 여부를 지정합니다.  
  
 **백분율 단위로 증가**  
 로그 파일의 증가 단위(백분율)를 지정합니다.  
  
 **크기 단위로 증가**  
 로그 파일의 증가 단위(MB)를 지정합니다.  

### <a name="more-info"></a>추가 정보
이 페이지에 표시되는 파일 크기 옵션에 대한 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요. 

## <a name="whats-next"></a>다음 단계  
 마법사에서 만들 새 데이터베이스의 이름을 지정하고 **확인**을 클릭하면 **데이터베이스 만들기** 대화 상자에서 **대상 선택** 페이지로 돌아갑니다. 자세한 내용은 [대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  

