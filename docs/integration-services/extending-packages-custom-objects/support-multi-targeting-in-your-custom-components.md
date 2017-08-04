---
title: "사용자 지정 구성 요소에서 다중 대상 지정 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bf7649b06354bfa621624ddfcf22bdea90bf0467
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>사용자 지정 구성 요소에서 다중 대상 지정을 지원 합니다.
 이제 사용할 수 있습니다 SSIS 디자이너 SQL Server Data Tools (SSDT) 만들기, 유지 관리 및 해당 대상 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012에는 패키지를 실행 합니다. Visual Studio 2015 용 SSDT를 다운로드 하려면 참조 [최신 SQL Server Data Tools 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)합니다. 

 솔루션 탐색기에서 Integration Services 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 프로젝트에 대한 속성 페이지를 엽니다. **구성 속성** 의 **일반**탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
   
 ![프로젝트 속성 대화 상자에서 TargetServerVersion 속성](../../integration-services/media/targetserverversion2.png "프로젝트 속성 대화 상자에서 TargetServerVersion 속성")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>여러 버전 지원 및 사용자 지정 구성 요소에 대 한 다중 대상 지정
 
모든 유형의 다섯 개의 사용자 지정 SSIS 확장 멀티 타기 팅을 지원합니다.
-   연결 관리자
-   태스크
-   열거자
-   로그 공급자
-   데이터 흐름 구성 요소

관리 되는 확장에 대 한 SSIS 디자이너에 지정 된 대상 버전에 대 한 확장의 버전을 로드합니다. 예를 들어
-   대상 버전이 SQL Server 2012 때 디자이너에서 확장의 2012 버전을 로드 합니다.
-   대상 버전이 SQL Server 2016 때 디자이너 2016 버전의 확장을 로드 합니다.

COM 확장 멀티 타기 팅을 지원 하지 않습니다. SSIS 디자이너는 항상 지정 된 대상 버전에 관계 없이 SQL Server의 현재 버전에 대 한 COM 확장을 로드합니다.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>여러 버전 및 다중 대상 지정에 대 한 기본 지원을 추가 합니다.

기본 지침 참조 [SQL Server 2016 용 SSDT 2015 년의 다중 버전 지원에 지원을 받기 위해 SSIS 사용자 지정 확장 프로그램을 가져오는](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)합니다. 이 블로그 게시물에서 다음 단계 또는 요구 사항에 설명 합니다.

-   해당 폴더에 어셈블리를 배포 합니다.

-   SQL Server 2014 및 높은 버전에 대 한 확장 맵 파일을 만듭니다.

## <a name="add-code-to-switch-versions"></a>버전을 전환 하는 코드를 추가 합니다.

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>사용자 지정 연결 관리자, 작업, 열거자, 또는 로그 공급자의 버전을 전환

사용자 지정 연결 관리자, 태스크, 열거자, 또는 로그 공급자를 추가에서 다운 그레이드 논리는 **의 SaveToXML** 메서드.

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>사용자 지정 데이터 흐름 구성 요소의 버전을 전환 합니다.

사용자 지정 연결 관리자, 태스크, 열거자, 또는 로그 공급자에 대 한 새에서 다운 그레이드 논리를 추가할 **PerformDowngrade** 메서드.

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>일반 오류

### <a name="invalidcastexception"></a>InvalidCastException

**오류 메시지입니다.** 형식의 캐스트 COM 개체 수 없습니다. 'System.__ComObject' 인터페이스에 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'를 입력합니다. 다음 오류로 인해 IID가 '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' 인 인터페이스의 COM 구성 요소에서 QueryInterface를 호출 하지 못했습니다이 작업에 실패 했습니다: 인터페이스 (HRESULT의 예외: 0x80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap)입니다.

**솔루션입니다.** 예: Microsoft.SqlServer.DTSPipelineWrap 또는 Microsoft.SqlServer.DTSRuntimeWrap SSIS interop 어셈블리를 참조 하는 사용자 지정 확장 프로그램의 값을 설정할는 **Interop 형식 포함** 속성을 * * False "입니다.

![Interop 형식 포함](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>대상 버전이 SQL Server 2012 때 일부 형식은 로드할 수 없습니다.

이 문제는 IErrorReportingService 또는 IUserPromptService와 같은 특정 유형에 영향을 줍니다.

**오류 메시지 (예:)입니다.** 어셈블리에서 'Microsoft.DataWarehouse.Design.IErrorReportingService' 형식을 로드할 수 없습니다 ' Microsoft.DataWarehouse, 버전 = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91'.

**해결 방법입니다.** 대상 버전을 SQL Server 2012에는 이러한 인터페이스 대신 MessageBox를 사용 합니다.


