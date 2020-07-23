---
title: Excel 연결 관리자 | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdac3f09fa3b92d7babd9c43f5a71adc4191ac7e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923725"
---
# <a name="excel-connection-manager"></a>Excel 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Excel 연결 관리자를 사용하면 패키지에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서 파일에 연결할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함되는 Excel 원본과 Excel 대상에서 Excel 연결 관리자가 사용됩니다.  
 
> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

 패키지에 Excel 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 Excel 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **EXCEL**로 설정됩니다.  
  
## <a name="configure-the-excel-connection-manager"></a>Excel 연결 관리자 구성  
 다음과 같은 방법으로 Excel 연결 관리자를 구성할 수 있습니다.  
  
-   Excel 통합 문서 파일의 경로를 지정합니다.  
  
-   파일을 만드는 데 사용된 Excel 버전을 지정합니다.  
  
-   선택한 워크시트 또는 범위에서 첫 데이터 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [Excel 연결 관리자 편집기](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="excel-connection-manager-editor"></a>Excel 연결 관리자 편집기
  **Excel 연결 관리자 편집기** 대화 상자를 사용하여 기존 또는 새 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서 파일에 대한 연결을 추가할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **Excel 파일 경로**  
 기존 또는 새 Excel 통합 문서 파일의 경로와 파일 이름을 입력합니다.  
   
 **찾아보기**  
 **열기** 대화 상자를 사용하여 Excel 파일이 있는 폴더 또는 새 파일을 만들려는 폴더로 이동합니다.  
  
 **Excel 버전**  
 파일을 만드는 데 사용된 Microsoft Excel 버전을 지정합니다.  
  
 **첫 행은 열 이름으로**  
 선택한 워크시트의 첫 데이터 행에 열 이름이 포함되는지 여부를 지정합니다. 이 옵션의 기본값은 **True**입니다.  

## <a name="solution-to-import-data-with-mixed-data-types-from-excel"></a>Excel에서 혼합 데이터 형식의 데이터를 가져오는 솔루션

혼합 데이터 형식의 데이터를 사용하는 경우 기본적으로 Excel 드라이버는 처음 8개 행(**TypeGuessRows** 레지스터 키로 구성)을 읽습니다. Excel 드라이버는 처음 8개 행의 데이터에 따라 각 열의 데이터 형식을 추측하려고 시도합니다. 예를 들어 Excel 데이터 원본에서 한 열에 숫자와 텍스트가 있는 경우 처음 8개 행에 숫자가 있으면 드라이버는 처음 8개 행에 따라 열 데이터가 정수 형식이라고 결정할 수 있습니다. 이 경우 SSIS는 텍스트 값을 건너뛰고 대상에 NULL로 가져옵니다.

이 문제를 해결하려면 다음 해결 방법 중 하나를 시도해 볼 수 있습니다.

* Excel 파일에서 Excel 열 형식을 **텍스트**로 변경합니다.
* 연결 문자열에 IMEX 확장 속성을 추가하여 드라이버의 기본 동작을 재정의합니다. 연결 문자열의 끝에 ";IMEX=1" 확장 속성을 추가하면 Excel에서 모든 데이터를 텍스트로 처리합니다. 다음 예제를 참조하십시오.
    
  ```ACE OLEDB connection string:
  Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\ExcelFileName.xlsx;Extended Properties="EXCEL 12.0 XML;HDR=YES;IMEX=1";
  ```

   이 솔루션이 안정적으로 작동하려면 레지스트리 설정을 수정해야 할 수도 있습니다. 기본 .cmd 파일은 다음과 같습니다.
  
   ```cmd
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   ```

* CSV 형식으로 파일을 저장하고 CSV 가져오기를 지원하도록 SSIS 패키지를 변경합니다.

## <a name="related-tasks"></a>관련 작업  
[SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
[Excel 원본](../data-flow/excel-source.md)  
[Excel 대상](../data-flow/excel-destination.md)
