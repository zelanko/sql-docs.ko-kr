---
title: 사용자 지정 구성 요소에서 멀티 타기팅 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4020d295bc29fa3d240c0176611d446fcb427197
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916391"
---
# <a name="support-multi-targeting-in-your-custom-components"></a>사용자 지정 구성 요소에서 멀티 타기팅 지원

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


 이제 SSDT(SQL Server Data Tools)에서 SSIS 디자이너를 사용하여 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 대상으로 하는 패키지를 만들고, 유지 관리하고, 실행할 수 있습니다. Visual Studio 2015용 SSDT를 다운로드하려면 [최신 SQL Server Data Tools 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요. 

 솔루션 탐색기에서 Integration Services 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 프로젝트에 대한 속성 페이지를 엽니다. **구성 속성** 의 **일반**탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
   
 ![프로젝트 속성 대화 상자의 TargetServerVersion 속성](../../integration-services/media/targetserverversion2.png "프로젝트 속성 대화 상자의 TargetServerVersion 속성")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>사용자 지정 구성 요소에 대한 여러 버전 지원 및 멀티 타기팅
 
다섯 가지 유형의 모든 SSIS 사용자 지정 확장은 멀티 타기팅을 지원합니다.
-   연결 관리자
-   작업
-   Enumerators
-   로그 공급자
-   데이터 흐름 구성 요소

관리되는 확장의 경우 SSIS 디자이너는 지정된 대상 버전에 대한 확장 버전을 로드합니다. 다음은 그 예입니다.
-   대상 버전이 SQL Server 2012인 경우 디자이너는 2012 버전의 확장을 로드합니다.
-   대상 버전이 SQL Server 2016인 경우 디자이너는 2016 버전의 확장을 로드합니다.

COM 확장은 멀티 타기팅을 지원하지 않습니다. SSIS 디자이너는 항상 지정된 대상 버전에 관계 없이 SQL Server의 현재 버전에 대한 COM 확장을 로드합니다.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>여러 버전 및 멀티 타기팅에 대한 기본 지원 추가

기본 지침은 [SQL Server 2016용 SSDT 2015의 다중 버전 지원으로 지원 받을 SSIS 사용자 지정 확장 가져오기](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)를 참조하세요. 이 블로그 게시물은 다음 단계 또는 요구 사항을 설명합니다.

-   적절한 폴더에 어셈블리를 배포합니다.

-   SQL Server 2014 이상 버전에 대한 확장 맵 파일을 만듭니다.

## <a name="add-code-to-switch-versions"></a>버전을 전환하는 코드 추가

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>사용자 지정 연결 관리자, 태스크, 열거자 또는 로그 공급자의 버전 전환

사용자 지정 연결 관리자, 태스크, 열거자 또는 로그 공급자의 경우 **SaveToXML** 메서드에서 다운그레이드 논리를 추가합니다.

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

### <a name="switch-versions-in-a-custom-data-flow-component"></a>사용자 지정 데이터 흐름 구성 요소에서 버전 전환

사용자 지정 연결 관리자, 태스크, 열거자 또는 로그 공급자의 경우 **PerformDowngrade** 메서드에서 다운그레이드 논리를 추가합니다.

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

**오류 메시지** 'System.__ComObject' 형식의 COM 개체를 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100' 인터페이스 유형으로 캐스트할 수 없습니다. 이 작업은 IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}'로 인터페이스에 대한 COM 구성 요소에 대한 QueryInterface 호출이 다음 오류: 지원되는 인터페이스 없음(HRESULT: 0x80004002(E_NOINTERFACE)에서 예외가 발생했습니다.)으로 인해 실패했으므로 실패했습니다. (Microsoft.SqlServer.DTSPipelineWrap).

**해결 방법** 사용자 지정 확장이 Microsoft.SqlServer.DTSPipelineWrap 또는 Microsoft.SqlServer.DTSRuntimeWrap와 같은 SSIS interop 어셈블리를 참조하는 경우 **Embed Interop Types** 속성의 값을 **False**로 설정합니다.

![Interop 형식 포함](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>대상 버전이 SQL Server 2012인 경우 일부 형식을 로드할 수 없습니다.

이 문제는 IErrorReportingService 또는 IUserPromptService와 같은 특정 유형에 영향을 줍니다.

**오류 메시지(예)** 어셈블리 'Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'에서 'Microsoft.DataWarehouse.Design.IErrorReportingService' 형식을 로드할 수 없습니다.

**해결 방법** 대상 버전이 SQL Server 2012인 경우 이러한 인터페이스 대신 MessageBox를 사용합니다.

