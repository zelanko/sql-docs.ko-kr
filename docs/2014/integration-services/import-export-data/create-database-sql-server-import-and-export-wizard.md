---
title: 데이터베이스 만들기(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 472daf928c92c69ab330ae1d77e6a6021c96e04f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250493"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>데이터베이스 만들기(SQL Server 가져오기 및 내보내기 마법사)
  **데이터베이스 만들기** 페이지를 사용하여 대상 파일에 대한 새 데이터베이스를 정의할 수 있습니다.  
  
 이 페이지에서는 새 데이터베이스 생성에 사용할 수 있는 옵션의 하위 집합을 제공합니다. 모든 옵션을 보려면 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 이 마법사에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사 시작 옵션에 대 한 마법사를 성공적으로 실행 하는 데 필요한 권한에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사를 실행](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **이름**  
 대상 SQL Server 데이터베이스에 사용할 고유 이름을 제공합니다. SQL Server 규칙에 따라 이 데이터베이스의 이름을 지정해야 합니다.  
  
 **데이터 파일 이름**  
 데이터 파일의 이름을 표시합니다. 데이터 파일의 이름은 앞에서 제공한 데이터베이스 이름에서 파생됩니다.  
  
 **로그 파일 이름**  
 로그 파일의 이름을 표시합니다. 데이터 파일의 이름은 앞에서 제공한 데이터베이스 이름에서 파생됩니다.  
  
 **초기 크기 (데이터 파일)**  
 데이터 파일의 처음 크기(MB)를 지정합니다.  
  
 **증가 허용 안 함 (데이터 파일)**  
 데이터 파일이 지정한 처음 크기 이상으로 증가할 수 있는지 여부를 지정합니다.  
  
 **백분율 단위로 증가 (데이터 파일)**  
 데이터 파일의 증가 단위(백분율)를 지정합니다.  
  
 **크기 단위로 증가 (데이터 파일)**  
 데이터 파일의 증가 단위(MB)를 지정합니다.  
  
 **초기 크기 (로그 파일)**  
 로그 파일의 처음 크기(MB)를 지정합니다.  
  
 **증가 허용 안 함 (로그 파일)**  
 로그 파일이 지정한 처음 크기 이상으로 증가할 수 있는지 여부를 지정합니다.  
  
 **백분율 단위로 증가 (로그 파일)**  
 로그 파일의 증가 단위(백분율)를 지정합니다.  
  
 **크기 단위로 증가 (로그 파일)**  
 로그 파일의 증가 단위(MB)를 지정합니다.  
  
  
