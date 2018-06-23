---
title: SSIS 패키지 저장(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 71f0b516b53a7682665c54be4403c5d10a4e5417
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183886"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>SSIS 패키지 저장(SQL Server 가져오기 및 내보내기 마법사)
  사용 하 여는 **i S 패키지 저장** 페이지 이름, 설명 및 저장 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` 데이터베이스 또는.dtsx는 포함 된 파일 확장입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 마법사로 만든 패키지를 저장 하는 옵션이 제공 되지 않습니다.  
  
 이 마법사에 대 한 자세한 참조 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사를 시작 하기 위한 옵션에 대 한 및 마법사를 실행 하는 데 필요한 사용 권한에 대 한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **이름**  
 패키지에 사용할 고유 이름을 제공합니다.  
  
 **설명**  
 패키지에 대한 설명을 입력합니다. 해당 패키지의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **대상**  
 대상 보기 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 파일) 대상 파일에 대해 이전에 지정 된 합니다.  
  
## <a name="target-dynamic-options"></a>대상 동적 옵션  
  
### <a name="target--sql-server"></a>대상 = SQL Server  
 **서버 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 선택한 경우 대상 서버 이름을 입력하거나 선택합니다.  
  
 **Windows 인증 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 선택한 경우 Windows 통합 인증을 사용하여 서버에 연결할지 여부를 지정합니다. 이 방법은 기본적으로 사용되는 인증 방법입니다.  
  
 **SQL Server 인증 사용**  
 선택한 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상, SQL Server 인증을 사용 하 여 서버에 연결할지 여부를 지정 합니다.  
  
 **사용자 이름**  
 선택한 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상, SQL Server 인증 유형을 지정 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름입니다.  
  
 **암호**  
 선택한 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상, SQL Server 인증 유형을 지정 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호입니다.  
  
### <a name="target--file-system"></a>대상 = 파일 시스템  
 **파일 이름**  
 파일 대상을 선택한 경우 대상 파일의 경로를 입력하거나 **찾아보기** 단추를 사용합니다.  
  
 **찾아보기**  
 파일 대상을 선택한 경우 **패키지 저장** 대화 상자를 사용하여 대상 파일을 찾습니다.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 저장](../save-packages.md)  
  
  