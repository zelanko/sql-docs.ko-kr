---
title: "데이터 원본 (SSAS 다차원) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.impersonationinfo.f1
- sql13.asvs.connectionmanager.f1
- sql13.asvs.datasourcedesigner.f1
helpviewer_keywords:
- impersonation [Analysis Services]
- data sources [Analysis Services], creating
- security [Analysis Services], data source connections
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
caps.latest.revision: 61
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 715f23cb80c0de16697b3aa66a4fb07669ad169e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-data-source-ssas-multidimensional"></a>데이터 원본 만들기(SSAS 다차원)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 모델에서 데이터 원본 개체는 데이터를 처리하거나 가져올 데이터 원본에 대한 연결을 나타냅니다. 다차원 모델은 적어도 하나 이상의 데이터 원본 개체를 포함해야 하지만 더 추가하여 여러 데이터 웨어하우스의 데이터를 결합할 수 있습니다. 이 항목의 지침에 따라 모델에 대한 데이터 원본 개체를 만들 수 있습니다. 이 개체의 속성 설정에 대한 자세한 내용은 [데이터 원본 속성 설정&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)을 참조하세요.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [데이터 공급자 선택](#bkmk_provider)  
  
 [자격 증명 및 가장 옵션 설정](#bkmk_impersonation)  
  
 [연결 속성 보기 또는 편집](#bkmk_ConnectionString)  
  
 [데이터 원본 마법사를 사용하여 데이터 원본 만들기](#bkmk_steps)  
  
 [기존 연결을 사용하여 데이터 원본 만들기](#bkmk_connection)  
  
 [모델에 여러 개의 데이터 원본 추가](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> 데이터 공급자 선택  
 관리되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 또는 네이티브 OLE DB 공급자를 사용하여 연결할 수 있습니다. 일반적으로 더 나은 성능을 제공하기 때문에 SQL Server 데이터 원본에 권장되는 데이터 공급자는 SQL Server Native Client입니다.  
  
 Oracle 및 기타 타사 데이터 원본의 경우 해당 타사에서 네이티브 OLE DB 공급자를 제공하는지 여부를 확인하고 해당 공급자를 먼저 시도해 보십시오. 오류가 발생할 경우 연결 관리자에 나열된 다른 .NET 공급자 또는 네이티브 OLE DB 공급자 중 하나를 사용해 보십시오. 사용하는 데이터 공급자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 솔루션을 개발하고 실행하는 데 사용하는 모든 컴퓨터에 설치되어 있는지 확인하십시오.  
  
##  <a name="bkmk_impersonation"></a> 자격 증명 및 가장 옵션 설정  
 데이터 원본 연결에서는 일부 경우에 SQL Azure 데이터베이스 연결 시 SQL Server 인증과 같은 Windows 인증 또는 데이터베이스 관리 시스템에서 제공되는 인증 서비스를 사용할 수 있습니다. 지정하는 계정에는 원격 데이터베이스 서버에 대한 로그인 및 외부 데이터베이스에 대한 사용 권한이 있어야 합니다.  
  
### <a name="windows-authentication"></a>Windows 인증  
 Windows 인증을 사용하는 연결은 데이터 원본 디자이너의 **가장 정보** 탭에 지정됩니다. 이 탭을 사용하여 외부 데이터 원본에 연결할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 실행되는 계정 이름을 지정하는 가장 옵션을 선택합니다. 모든 시나리오에서 모든 옵션을 사용할 수 있지는 않습니다. 이러한 옵션 및 사용 시기에 대한 자세한 내용은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요.  
  
### <a name="database-authentication"></a>데이터베이스 인증  
 Windows 인증 대신 데이터베이스 관리 시스템에서 제공되는 인증 서비스를 사용하는 연결을 지정할 수 있습니다. 경우에 따라 데이터베이스 인증을 사용해야 합니다. 데이터베이스 인증을 사용하기 위한 시나리오에는 Windows Azure SQL Database 연결 시 SQL Server 인증 사용 또는 다른 운영 체제 또는 트러스트되지 않은 도메인에서 실행되는 관계형 데이터 원본 액세스가 포함됩니다.  
  
 데이터베이스 인증을 사용하는 데이터 원본의 경우 데이터베이스 로그인의 사용자 이름 및 암호가 연결 문자열에 지정됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모델에 데이터 원본 연결 설정 시 연결 관리자에 사용자 이름과 암호를 입력하면 연결 문자열에 자격 증명이 추가됩니다. 데이터 읽기 권한이 있는 사용자 ID를 지정해야 합니다.  
  
 데이터를 검색하는 경우 연결을 설정하는 클라이언트 라이브러리에서 연결 문자열에 자격 증명을 포함하는 연결 요청을 생성합니다. 가장 정보 탭의 Windows 인증 자격 증명 옵션은 연결에는 사용되지 않지만 로컬 컴퓨터의 리소스에 액세스 등 다른 작업에는 사용할 수 있습니다. 자세한 내용은 [가장 옵션 설정&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)을 참조하세요.  
  
 모델에서 데이터 원본 개체를 저장한 후 연결 문자열 및 암호가 암호화됩니다.  보안을 유지하기 위해 도구, 스크립트 또는 코드에서 암호를 볼 때 표시되는 모든 암호의 추적이 연결 문자열에서 제거됩니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서는 연결 문자열과 함께 암호를 저장하지 않습니다. 암호를 저장하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 필요한 경우 암호를 입력하라는 메시지를 표시합니다. 암호를 저장하면 해당 암호는 데이터 연결 문자열에 암호화된 형식으로 저장됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 데이터 원본이 포함된 데이터베이스의 데이터베이스 암호화 키를 사용하여 데이터 원본에 대한 암호 정보를 암호화합니다. 암호화된 연결 정보를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정이나 암호를 변경해야 하며 그렇지 않으면 암호화된 정보를 복구할 수 없습니다. 자세한 내용은 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)을 참조하세요.  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>데이터 마이닝 개체에 대한 가장 정보 정의  
 데이터 마이닝 쿼리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정의 컨텍스트에서 실행할 수 있지만 쿼리를 제출하는 사용자의 컨텍스트나 지정한 사용자의 컨텍스트에서 실행할 수도 있습니다. 쿼리가 실행되는 컨텍스트는 쿼리 결과에 영향을 줄 수도 있습니다. 데이터 마이닝 **OPENQUERY** 유형 작업에 대해 서비스 계정의 컨텍스트 대신 쿼리를 실행하는 사용자에 관계없이 현재 사용자의 컨텍스트나 지정한 사용자의 컨텍스트에서 데이터 마이닝 쿼리를 실행할 수 있습니다. 이렇게 하면 제한된 보안 자격 증명을 사용하여 쿼리를 실행할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 현재 사용자를 가장하거나 지정한 사용자를 가장하려면 **특정 사용자 이름 및 암호 사용** 또는 **현재 사용자의 자격 증명 사용** 옵션을 선택합니다.  
  
##  <a name="bkmk_steps"></a> 데이터 원본 마법사를 사용하여 데이터 원본 만들기  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 데이터 원본을 정의할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 열거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 연결합니다.  
  
2.  **솔루션 탐색기**에서 **데이터 원본** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터 원본** 을 클릭하여 **데이터 원본 마법사**를 시작합니다.  
  
3.  **연결 정의 방법 선택** 페이지에서 **기존 연결 또는 새 연결을 사용하여 데이터 원본 만들기** 를 선택한 다음 **새로 만들기** 를 클릭하여 **연결 관리자**를 엽니다.  
  
     새 연결은 연결 관리자에서 만듭니다. 연결 관리자에서 공급자를 선택한 다음 기본 데이터에 연결하기 위해 해당 공급자에 사용되는 연결 문자열 속성을 지정합니다. 실제 필요한 정보는 선택한 공급자에 따라 달라지지만 일반적으로 서버나 서버 인스턴스, 서버나 서버 인스턴스 로그온에 대한 정보, 데이터베이스나 파일 이름, 기타 공급자별 설정 등의 정보가 필요합니다. 이 절차의 남은 부분에서는 SQL Server 데이터베이스 연결을 사용합니다.  
  
4.  연결에 사용할 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 또는 네이티브 OLE DB 공급자를 선택합니다.  
  
     새 연결의 기본 공급자는 네이티브 OLE DB\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자입니다. 이 공급자는 OLE DB를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 인스턴스에 연결하는 데 사용됩니다. SQL Server 관계형 데이터베이스에 대한 연결의 경우 네이티브 OLE DB\SQL Server Native Client 11.0을 사용하면 다른 공급자를 사용할 때보다 더 빠른 경우가 많습니다.  
  
     다른 공급자를 선택하여 다른 데이터 원본에 액세스할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원하는 공급자 및 관계형 데이터베이스의 목록은 [지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)을 참조하세요.  
  
5.  기본 데이터 원본에 연결하기 위해 선택한 공급자가 요청한 정보를 입력합니다. **네이티브 OLE DB\SQL Server Native Client** 공급자를 선택한 경우 다음 정보를 입력합니다.  
  
    1.  **서버 이름** 은 데이터베이스 엔진 인스턴스의 네트워크 이름입니다. IP 주소, 컴퓨터의 NETBIOS 이름 또는 정규화된 도메인 이름으로 지정할 수 있습니다. 인스턴스 이름을 포함 해야는 서버가 명명 된 인스턴스로 설치 된 경우 (예를 들어 \<컴퓨터 이름 >\\< instancename\>).  
  
    2.  **서버에 로그온** 은 연결이 인증이 되는 방식을 지정합니다. **Windows 인증 사용** 은 Windows 인증을 사용합니다. **SQL Server 인증 사용** 은 혼합 모드 인증을 지원하는 Windows Azure SQL Database 또는 SQL Server 인스턴스의 데이터베이스 사용자 로그인을 지정합니다.  
  
        > [!IMPORTANT]  
        >  SQL Server 인증을 사용하는 연결의 경우 연결 관리자에 **암호 저장** 확인란이 포함됩니다. 이 확인란은 항상 표시되지만 항상 사용되지는 않습니다.  
        >   
        >  활성 Analysis Services 데이터베이스에 사용되는 SQL Server 관계형 데이터를 새로 고치거나 처리하는 경우에는 Analysis Services에서 이 확인란이 사용되지 않습니다. **암호 저장**의 선택 여부에 관계없이 Analysis Services에서는 항상 암호를 암호화하여 저장합니다. 암호는 .abf 파일과 데이터 파일에 암호화되어 저장됩니다. 이는 Analysis Services에서 서버의 세션 기반 암호 저장소를 지원하지 않기 때문입니다.  
        >   
        >  이 동작은 Analysis Services 서버 인스턴스에 보관되는 데이터베이스와 SQL Server 인증을 사용하여 관계형 데이터를 새로 고치거나 처리하는 데이터베이스에만 적용됩니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 설정되었으며 세션 기간 중에만 사용되는 데이터 원본 연결에는 적용되지 않습니다. 이미 저장된 암호는 제거할 수 없지만 다른 자격 증명 또는 Windows 인증을 사용하여 현재 데이터베이스와 함께 저장된 사용자 정보를 덮어쓸 수는 있습니다.  
  
    3.  **데이터베이스 이름 선택 또는 입력** 또는 **데이터베이스 파일 첨부** 는 데이터베이스를 지정하는 데 사용됩니다.  
  
    4.  대화 상자의 왼쪽에서 **모두** 를 클릭하여 이 공급자의 모든 기본 설정을 비롯한 이 연결의 추가 설정을 표시합니다.  
  
    5.  환경에 맞게 설정을 변경한 다음 **확인**을 클릭합니다.  
  
         데이터 원본 마법사의 **연결 정의 방법 선택** 페이지에 있는 **데이터 연결** 창에 새 연결이 나타납니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **가장 정보**에서 외부 데이터 원본에 연결할 때 Analysis Services에서 사용하는 Windows 자격 증명 또는 사용자 ID를 지정합니다. 데이터베이스 인증을 사용하는 경우에는 연결 목적에 대해 이러한 설정이 무시됩니다.  
  
     가장 옵션의 선택 지침은 데이터 원본을 사용하는 방법에 따라 다릅니다. 처리 태스크의 경우 데이터 원본에 연결할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 서비스 계정이나 지정한 사용자 계정의 보안 컨텍스트에서 실행해야 합니다.  
  
    -   **특정 Windows 사용자 이름 및 암호 사용** 을 사용하면 고유한 최소 권한 자격 증명 집합을 지정할 수 있습니다.  
  
    -   **서비스 계정 사용** 을 사용하면 서비스 ID를 사용하여 데이터를 처리할 수 있습니다.  
  
     지정한 계정에는 데이터 원본에 대한 읽기 권한이 있어야 합니다.  
  
8.  **다음**을 클릭합니다.  **마법사 완료**에서 데이터 원본 이름을 입력하거나 기본 이름을 사용합니다. 기본 이름은 연결에 지정된 데이터베이스의 이름입니다. **미리 보기** 창에 새 데이터 원본의 연결 문자열이 표시됩니다.  
  
9. **마침**을 클릭합니다.  솔루션 탐색기의 **데이터 원본** 폴더에 새 데이터 원본이 나타납니다.  
  
##  <a name="bkmk_connection"></a> 기존 연결을 사용하여 데이터 원본 만들기  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 작업을 수행하는 경우 데이터 원본은 솔루션의 기존 데이터 원본이나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 기반으로 만들 수 있습니다. 데이터 원본 마법사는 같은 프로젝트의 기존 연결을 사용하는 방법을 포함하여 데이터 원본 개체를 만들기 위한 몇 가지 옵션을 제공합니다.  
  
-   솔루션의 기존 데이터 원본을 사용하여 데이터 원본을 만들면 기존 데이터 원본과 동기화되는 데이터 원본을 정의할 수 있습니다. 이 새 데이터 원본이 포함된 프로젝트가 작성되면 기본 데이터 원본의 데이터 원본 설정이 사용됩니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 사용하여 데이터 원본을 만들면 현재 프로젝트에서 솔루션의 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 참조할 수 있습니다. 새 데이터 원본은 선택한 프로젝트의 **Data Source** 및 **Initial Catalog** 속성에서 얻은 **TargetServer** 속성 및 **TargetDatabase** 속성으로 MSOLAP 공급자를 사용합니다. 원본 및 대상 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에는 원격 파티션 저장 및 처리 지원을 위해 상호 데이터 원본이 필요하므로 이 기능은 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 사용하여 원격 파티션을 관리하는 솔루션에 유용합니다.  
  
 데이터 원본 개체를 참조하는 경우 참조된 개체나 프로젝트에서만 해당 개체를 편집할 수 있습니다. 참조가 포함된 데이터 원본 개체의 연결 정보는 편집할 수 없습니다. 참조된 개체나 프로젝트의 연결 정보를 변경하면 작성되는 새 데이터 원본에도 변경 내용이 나타납니다. 프로젝트의 데이터 원본 파일(.ds)에 나타나는 연결 문자열 정보는 프로젝트를 빌드하거나 데이터 원본 디자이너에서 해당 참조를 지울 때 동기화됩니다.  
  
##  <a name="bkmk_ConnectionString"></a> 연결 속성 보기 또는 편집  
 연결 문자열은 데이터 원본 디자이너 또는 새 데이터 원본 마법사에서 선택하는 속성을 기반으로 공식화됩니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 연결 문자열 및 기타 속성을 볼 수 있습니다.  
  
 **연결 문자열을 편집하려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서는 솔루션 탐색기에서 데이터 원본 개체를 두 번 클릭합니다.  
  
2.  **편집**을 클릭한 다음 왼쪽 탐색 창에서 **모두** 를 클릭합니다.  
  
3.  속성표가 나타나고, 사용 중인 데이터 데이터 공급자의 사용 가능한 속성이 표시됩니다. 이 속성에 대한 자세한 내용은 공급자의 제품 설명서를 참조하십시오.  SQL Server Native Client의 경우 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 솔루션에 여러 데이터 원본 개체가 있고 연결 문자열을 한 곳에 유지하려는 경우 현재 데이터 원본이 다른 데이터 원본 개체를 참조하도록 구성할 수 있습니다.  
  
 *데이터 원본 참조* 는 같은 솔루션에 있는 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 데이터 원본에 대한 연결입니다. 참조는 단일 솔루션의 개체 간에 데이터 원본을 동기화하는 방법을 제공합니다. 연결 문자열 정보는 프로젝트를 빌드할 때마다 동기화됩니다. 다른 개체를 참조하는 데이터 원본에 대한 연결 문자열을 변경하려면 참조되는 개체의 연결 문자열을 변경해야 합니다.  
  
 확인란 선택을 취소하여 참조를 제거할 수 있습니다. 그러면 개체 간 동기화가 종료되므로 데이터 원본의 연결 문자열을 변경할 수 있습니다.  
  
##  <a name="bkmk_multipleDS"></a> 모델에 여러 개의 데이터 원본 추가  
 추가 데이터 원본에 대한 연결을 지원하기 위한 두 개 이상의 데이터 원본 개체를 만들 수 있습니다. 각 데이터 원본에는 관계를 만드는 데 사용할 수 있는 열이 있어야 합니다.  
  
> [!NOTE]  
>  여러 데이터 원본이 정의되어 있고 눈송이 차원에 대한 경우와 같이 단일 쿼리로 여러 원본의 데이터를 쿼리하는 경우 **OpenRowset**을 사용하여 원격 쿼리를 지원하는 데이터 원본을 정의해야 합니다. 일반적으로 Microsoft SQL Server 데이터 원본이 사용됩니다.  
  
 여러 데이터 원본을 사용하기 위한 요구 사항에는 다음과 같은 내용이 포함됩니다.  
  
-   하나의 데이터 원본을 주 데이터 원본으로 지정합니다. 주 데이터 원본은 데이터 원본 뷰를 만드는 데 사용되는 데이터 원본입니다.  
  
-   주 데이터 원본은 **OpenRowset** 함수를 지원해야 합니다.  SQL Server의 이 함수에 대한 자세한 내용은 <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>을 참조하세요.  
  
 다음 방법을 사용하여 여러 데이터 원본의 데이터를 결합할 수 있습니다.  
  
1.  모델에 데이터 원본을 만듭니다.  
  
2.  SQL Server 관계형 데이터베이스를 데이터 원본으로 사용하여 데이터 원본 뷰를 만듭니다. 이것이 주 데이터 원본입니다.  
  
3.  데이터 원본 뷰 디자이너에서 방금 만든 데이터 원본 뷰를 사용하는 작업 영역을 마우스 오른쪽 단추로 클릭하고 **테이블 추가/제거**를 선택합니다.  
  
4.  두 번째 데이터 원본을 선택한 다음 추가할 테이블을 선택합니다.  
  
5.  추가한 테이블을 찾아 선택합니다. 테이블을 마우스 오른쪽 단추로 클릭하고 **새 관계**를 선택합니다. 일치하는 데이터가 들어 있는 원본 열과 대상 열을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

