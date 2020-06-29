---
title: SQL Server 가져오기 및 내보내기 마법사 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b1803dd3357d2a725f2196e2c692f7470e27a03f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436860"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사 실행
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 데이터 원본 간에 데이터를 복사하고 기본 패키지를 구성하는 가장 간단한 방법을 제공합니다. 마법사에 대 한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조 하세요.  
  
 SQL Server 가져오기 및 내보내기 마법사를 사용 하 여 SQL Server 데이터베이스에서 Microsoft Excel 스프레드시트로 데이터를 내보내는 패키지를 만드는 방법을 보여 주는 비디오는 [Excel로 SQL Server 데이터 내보내기 (SQL Server 비디오)](https://go.microsoft.com/fwlink/?LinkId=131024)를 참조 하십시오.  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 시작하려면  
  
-   **시작** 메뉴에서 **모든 프로그램**,**Microsoft SQL Server** 을 차례로 가리킨 다음 **데이터 가져오기 및 내보내기**를 클릭 합니다.  
  
     또는  
  
     에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **SSIS 패키지** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **SSISImport 및 내보내기 마법사**를 클릭 합니다.  
  
     또는  
  
     의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **프로젝트** 메뉴에서 **SSISImport 및 내보내기 마법사**를 클릭 합니다.  
  
     또는  
  
     에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서버 유형에 연결 하 고 데이터베이스 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 확장 한 다음 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **태스크**를 가리킨 다음 **데이터 가져오기** 또는 **데이터 내보내기**를 클릭 합니다.  
  
     또는  
  
     명령 프롬프트 창에서 C:\Program Files\Microsoft SQL Server\100\DTS\Binn에 있는 DTSWizard.exe를 실행합니다.  
  
    > [!NOTE]  
    >  64비트 컴퓨터의 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 64비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사(DTSWizard.exe)를 설치합니다. 그러나 Access 또는 Excel 등의 일부 데이터 원본은 32비트 공급자만 제공합니다. 이러한 데이터 원본을 사용하려면 32비트 버전의 마법사를 설치하여 실행해야 합니다. 32비트 버전의 마법사를 설치하려면 설치 도중 클라이언트 도구 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 선택합니다.  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터를 가져오거나 내보내려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  해당 마법사 페이지에서 데이터 원본 및 데이터 대상을 선택합니다.  
  
     사용 가능한 데이터 원본에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자, OLE DB 공급자, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자, [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자, Microsoft Office Excel, Microsoft Office Access 및 플랫 파일 원본이 포함됩니다. 원본에 따라 인증 모드, 서버 이름, 데이터베이스 이름 및 파일 형식과 같은 옵션을 설정합니다.  
  
    > [!NOTE]  
    >  Oracle용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB 공급자는 Oracle BLOB, CLOB, NCLOB, BFILE 및 UROWID 데이터 형식을 지원하지 않습니다. 따라서 OLE DB 원본은 이러한 데이터 형식의 열이 포함된 테이블의 데이터를 추출할 수 없습니다.  
  
     사용 가능한 데이터 대상에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자, OLE DB 공급자, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, Excel, Access 및 플랫 파일 대상이 포함됩니다.  
  
3.  선택한 대상 유형에 따라 옵션을 설정합니다.  
  
     대상이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스인 경우 다음을 지정할 수 있습니다.  
  
    -   새 데이터베이스를 만들고 데이터베이스 속성을 설정할지 여부를 나타냅니다. 다음 속성은 구성할 수 없으며 마법사에서 지정된 기본값이 사용됩니다.  
  
        |속성|값|  
        |--------------|-----------|  
        |데이터 정렬|Latin1_General_CS_AS_KS_WS|  
        |복구 모델|전체|  
        |전체 텍스트 인덱싱 사용|True|  
  
    -   테이블 또는 뷰에서 데이터를 복사할지, 아니면 쿼리 결과를 복사할지를 선택합니다.  
  
         원본 데이터를 쿼리하고 결과를 복사하려는 경우 Transact-SQL 쿼리를 구성할 수 있습니다. Transact-SQL 쿼리를 수동으로 입력하거나 파일에 저장된 쿼리를 사용할 수 있습니다. 마법사에는 파일을 찾기 위한 찾아보기 기능이 있으며, 파일을 선택하면 마법사가 자동으로 파일을 열고 파일 내용을 마법사 페이지에 붙여 넣습니다.  
  
         원본이 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자인 경우 쿼리 결과를 복사하는 옵션을 사용하여 DBCommand 문자열을 쿼리로 제공할 수도 있습니다.  
  
         원본 데이터가 뷰이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기/내보내기 마법사가 자동으로 뷰를 대상의 테이블로 변환합니다.  
  
    -   대상 테이블을 삭제한 다음 다시 만들지 여부와 ID 삽입을 사용할지 여부를 나타냅니다.  
  
    -   기존 대상 테이블에서 행을 삭제하거나 추가할지 여부를 나타냅니다. 테이블이 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사가 테이블을 자동으로 만듭니다.  
  
     대상이 플랫 파일 대상인 경우에는 다음을 지정할 수 있습니다.  
  
    -   대상 파일의 행 구분 기호를 지정합니다.  
  
    -   대상 파일의 열 구분 기호를 지정합니다.  
  
4.  필요에 따라 테이블 한 개를 선택하고 원본 열과 대상 열 사이의 매핑을 변경하거나 대상 열의 메타데이터를 변경합니다.  
  
    -   원본 열을 다른 대상 열로 매핑합니다.  
  
    -   대상 열의 데이터 형식을 변경합니다.  
  
    -   문자 데이터 형식이 포함된 열의 길이를 설정합니다.  
  
    -   숫자 데이터 형식이 포함된 열의 전체 자릿수와 소수 자릿수를 설정합니다.  
  
    -   열에 대한 Null 값 허용 여부를 지정합니다.  
  
5.  필요에 따라 여러 테이블을 선택하고 메타데이터 및 옵션을 업데이트하여 해당 테이블에 적용합니다.  
  
    -   기존 대상 스키마를 선택하거나 테이블을 할당할 새 스키마를 제공합니다.  
  
    -   대상 테이블에 ID를 삽입할 수 있도록 할지 여부를 지정합니다.  
  
    -   대상 테이블을 삭제하고 다시 만들지 여부를 지정합니다.  
  
    -   기존 대상 테이블을 자를지 여부를 지정합니다.  
  
6.  패키지를 저장하고 실행합니다.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 명령 프롬프트에서 마법사를 시작한 경우 패키지를 즉시 실행할 수 있습니다. 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스 또는 파일 시스템에 패키지를 저장할 수 있습니다. **Msdb** 데이터베이스에 대 한 자세한 내용은 [SSIS 서비스&#41;패키지 관리 &#40;](../service/package-management-ssis-service.md)를 참조 하세요.  
  
     패키지를 저장할 때 패키지 보호 수준을 설정할 수 있으며 설정한 보호 수준에서 암호가 사용되는 경우 암호를 제공할 수 있습니다. 패키지 보호 수준에 대 한 자세한 내용은 [패키지의 중요 한 데이터에 대 한 Access Control](../security/access-control-for-sensitive-data-in-packages.md)를 참조 하세요.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트에서 마법사를 시작한 경우 마법사에서 패키지를 실행할 수 없습니다. 대신 마법사를 시작한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 패키지가 추가됩니다. 그런 다음 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행할 수 있습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에서는 마법사가 만든 패키지를 저장하는 옵션을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [SQL Server Data Tools에서 패키지 만들기](../create-packages-in-sql-server-data-tools.md)  
  
  
