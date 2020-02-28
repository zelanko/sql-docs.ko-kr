---
title: 연장 보안 업데이트 정의
description: 'SQL Server 레지스트리를 사용하여 지원 종료 및 수명 종료 SQL Server 제품(예: SQL Server 2008 및 SQL Server 2008 R2)에 대한 연장 보안 업데이트를 얻는 방법을 알아봅니다.'
ms.custom: ''
ms.date: 12/09/2019
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ac74f1af3d570863bafae7185d6d4ce653f1f036
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256734"
---
# <a name="what-are-extended-security-updates-for-sql-server"></a>SQL Server의 연장 보안 업데이트란 무엇입니까?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 레지스트리 서비스를 사용하여 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 대한 연장 보안 업데이트를 얻는 정보를 제공합니다. 다른 옵션에 대한 자세한 내용은 [지원 종료 옵션](sql-server-end-of-life-overview.md)을 참조하세요. 

## <a name="overview"></a>개요
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지원 수명 주기의 끝에 도달하면 서버에 대한 ESU(연장 보안 업데이트) 구독에 등록하고 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하거나 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 마이그레이션할 때까지 최대 3년 동안 보호된 상태로 유지하는 옵션이 제공됩니다. 이 구독은 다음과 같은 두 가지 방법으로 사용할 수 있습니다.
-  온-프레미스 또는 호스티드 환경 서버에서 구매할 수 있습니다.
-  별도의 비용 없이 온-프레미스 서버를 Azure Virtual Machines로 마이그레이션할 때 기본적으로 사용하도록 설정됩니다. 그런 다음 Azure Portal의 **SQL Server 레지스트리** 서비스를 사용하여 지원 종료 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하고 업데이트를 사용할 수 있게 되면 업데이트를 다운로드할 수 있습니다. 

ESU 패치는 제공되는 즉시 적용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 보호하는 것이 좋습니다. ESU에 대한 자세한 내용은 [ESU FAQ 페이지](https://www.microsoft.com/cloud-platform/extended-security-updates)를 참조하세요.

> [!IMPORTANT]
> [SQL Server 2008 및 SQL Server 2008 R2에 대한 확장 지원은 2019년 7월 10일에 종료](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)되었습니다. 이러한 버전의 경우 이 문서에 설명된 연장 보안 업데이트 또는 다른 마이그레이션 옵션을 사용하는 것이 좋습니다. 자세한 내용은 [지원 종료 옵션](sql-server-end-of-life-overview.md)을 참조하세요.

## <a name="what-are-extended-security-updates"></a>연장 보안 업데이트 정의
[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 대한 ESU(연장 보안 업데이트)는 확장 지원 업데이트 구독을 구매한 고객에 대한 보안 업데이트 프로비전을 포함합니다.

[MSRC(Microsoft 보안 대응 센터)](https://portal.msrc.microsoft.com)에 의해 보안 취약성이 발견되어 **중요**로 평가되면 **필요한 경우** ESU를 사용할 수 있습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ESU에 대한 정기 릴리스 주기가 없습니다.

ESU에는 다음이 포함되지 않습니다.
- 새로운 기능
- 기능 향상
- 고객이 요청한 픽스

### <a name="support"></a>지원
ESU에는 기술 지원이 포함되지 않지만, 온-프레미스를 유지하기로 선택하는 경우 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] / [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 에 대한 [소프트웨어 지원](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default?activetab=software-assurance-default-pivot%3aprimaryr3) 또는 프리미어/통합 지원과 같은 활성 지원 계약을 사용하여 ESU에 포함된 워크로드에 대한 기술 지원을 받을 수 있습니다. 또는 Azure에서 호스트하는 경우 Azure 지원 플랜을 사용하여 기술 지원을 받을 수 있습니다. 

  > [!NOTE]
  > Microsoft는 (온-프레미스와 호스팅 환경 모두에서) ESU 구독에 포함되지 않은 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 인스턴스에 대한 기술 지원을 제공할 수 없습니다. 

## <a name="esu-availability-and-deployment"></a>ESU 가용성 및 배포
Azure, 온-프레미스 또는 호스팅 환경에서 워크로드를 실행하는 고객은 ESU를 사용할 수 있습니다.

### <a name="azure-virtual-machines"></a>Azure Virtual Machines
워크로드를 Azure Virtual Machines(IaaS)로 마이그레이션하는 경우 지원 종료 후 최대 3년 동안 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 대한 연장 보안 업데이트에 액세스할 수 있으며, 이 경우에는 가상 머신을 실행하는 비용 이외에 **추가 요금**이 발생하지 않습니다. 고객은 Azure에서 연장 보안 업데이트를 받기 위해 소프트웨어 보증이 필요하지 않습니다. 

**Windows Server 2008 R2 이상**에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 Azure Virtual Machines는 가상 머신이 [자동화된 패치](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)를 사용하여 구성된 경우 기존의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트 채널을 통해 자동으로 ESU를 수신합니다.

**Windows Server 2008**에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 실행하는 Azure VM(가상 머신) 또는 **[자동화된 패치](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)에 대해 구성되지 않은** VM은 [온-프레미스 또는 호스티드 환경](#on-premises-or-hosted-environments) 섹션에서 설명한 대로 ESU 패치를 수동으로 다운로드하여 배포해야 합니다. 

### <a name="on-premises-or-hosted-environments"></a>온-프레미스 또는 호스티드 환경
Software Assurance가 있는 경우 EA(기업계약), EAS(기업 정기가입 계약), SCE(서버 및 클라우드 등록) 또는 EES(교육 솔루션 등록)에 따라 지원 종료일 이후 최대 3년간 ESU(연장된 보안 업데이트)를 구매할 수 있습니다. 적용해야 하는 서버에 대한 ESU만 구매할 수 있습니다. Microsoft 또는 Microsoft 라이선스 파트너에서 직접 ESU를 구매할 수 있습니다. 

ESU 계약이 적용되는 고객은 다음 단계를 수행하여 ESU 패치를 다운로드하고 배포해야 합니다.
-  **[SQL Server 레지스트리](#create-sql-server-registry)** 에서 [적격 인스턴스](#register-instances-for-esus)를 등록합니다. 
-  등록되면 ESU 패치가 출시될 때마다 패키지를 다운로드할 수 있도록 Azure Portal에서 다운로드 링크가 제공됩니다. 
-  다운로드된 패키지를 온-프레미스 또는 호스티드 환경에 수동으로 배포할 수도 있고, 조직에서 사용하는 업데이트 오케스트레이션 솔루션(예: Microsoft Endpoint Configuration Manager(이전의 System Center Configuration Manager))을 통해 배포할 수도 있습니다. 

> [!NOTE]
> 이는 자동 업데이트를 수신하도록 구성되지 않은 Azure Stack 및 Azure Virtual Machines에 대해 고객이 따라야 하는 프로세스이기도 합니다.

자세한 내용은 [연장 보안 업데이트 FAQ](https://www.microsoft.com/cloud-platform/extended-security-updates)를 참조하세요. 

## <a name="create-sql-server-registry"></a>SQL Server 레지스트리 만들기
ESU 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하려면 먼저 Azure Portal에 SQL Server 레지스트리를 만들어야 합니다. 

> [!IMPORTANT]
> [자동 업데이트](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)에 대해 구성된 Azure 가상 머신을 실행할 때는 ESU에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하지 않아도 됩니다. 

SQL Server 레지스트리를 만들려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. 
1. **리소스 만들기** 옵션을 선택하여 리소스를 만듭니다. 
1. 검색 상자에 `SQL Server registry`를 입력합니다.  
1. [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 게시한 **SQL Server 레지스트리** 옵션을 선택한 다음 **만들기**를 선택합니다. 

   ![SQL Server 레지스트리 서비스를 선택합니다.](media/sql-server-extended-security-updates/sql-server-registry-service.png)

1. **프로젝트 세부 정보**의 드롭다운에서 구독을 선택합니다. 그런 다음 기존 **리소스 그룹**을 선택하거나 **새로 만들기**를 선택하여 새 SQL Server 레지스트리 서비스에 대한 새 리소스 그룹을 만듭니다. 
1. **서비스 세부 정보**에서 새 **SQL Server 레지스트리** 리소스의 이름과 지역을 제공합니다. 

   ![SQL Server 레지스트리 서비스를 선택합니다.](media/sql-server-extended-security-updates/create-new-sql-server-registry.png)

1. **검토 + 만들기**를 선택하여 **SQL Server 레지스트리**에 대한 세부 정보를 검토합니다. 유효성 검사가 성공하면 **만들기**를 선택합니다. 

## <a name="register-instances-for-esus"></a>ESU용 인스턴스 등록

**SQL Server 레지스트리** 리소스가 배포된 후 [단일](#single-sql-server-instance) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하도록 선택하거나 [대량](#multiple-sql-server-instances-in-bulk)에서 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록할 수 있습니다. ESU 패키지를 다운로드하려면 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 SQL Server 레지스트리의 범위에 등록되어 있어야 합니다. 

### <a name="single-sql-server-instance"></a>단일 SQL Server 인스턴스

단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. 
1. **SQL Server 레지스트리** 리소스로 이동합니다. 
1. **개요** 창에서 **+ 등록**을 선택합니다. 

   ![등록을 선택하여 SQL Server의 단일 인스턴스를 등록](media/sql-server-extended-security-updates/register-single-sql-server-instance.png)

1. 이 표에 설명된 대로 필요한 정보를 입력한 다음 **등록**을 선택합니다. 

   |**값**| **설명**|
   | :-------| :------------- |
   | **인스턴스** | 명령 `SELECT @@SERVERNAME`(`MyServer\Instance01`)의 출력을 입력합니다. | 
   | **SQL 버전** | 드롭다운에서 2008 또는 2008 R2를 선택합니다. | 
   | **버전(Edition)** | 드롭다운에서 해당하는 버전을 선택합니다. Datacenter, Developer(ESU를 구매한 경우 무료로 배포), Enterprise, Standard, Web, Workgroup. | 
   | **코어 수** | 이 인스턴스의 코어 수를 입력합니다. | 
   | **호스트 유형** | 드롭다운에서 해당하는 호스트 유형을 선택합니다. 가상 머신(온-프레미스), 물리적 서버(온-프레미스), Azure Virtual Machine, Amazon EC2, Google Compute Engine, 기타. |
   | **SubscriptionID**<sup>1</sup> | VM이 생성되는 SubscriptionID를 입력합니다.  |
   | **리소스 그룹**<sup>1</sup> | VM이 생성되는 리소스 그룹을 입력합니다.  | 
   | **Azure VM 이름**<sup>1</sup>  | VM 리소스 이름을 입력합니다.  | 
   | **Azure VM 운영 체제**<sup>1</sup> | 드롭다운에서 적용 가능한 Windows Server 운영 체제 버전을 선택합니다. | 

   <sup>1</sup> Azure 가상 머신에만 필요합니다. 

이제 새로 등록된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 **개요** 창의 **SQL Server 인스턴스 등록** 섹션에 표시됩니다. 

![등록된 SQL Server 인스턴스](media/sql-server-extended-security-updates/registered-sql-instance.png)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하면 **보안 업데이트** 섹션을 사용할 수 있게 됩니다. 사용 가능한 ESU가 모두 게시됩니다. 

### <a name="multiple-sql-server-instances-in-bulk"></a>대량으로 여러 SQL Server 인스턴스

.CSV 파일을 업로드하여 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 대량으로 등록할 수 있습니다. [.CSV 파일의 형식이 올바르게 지정](#formatting-requirements-for-csv-file)되었으면 다음 단계에 따라 SQL Server 레지스트리 리소스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 대량 등록할 수 있습니다. 

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. 
1. **SQL Server 레지스트리** 리소스로 이동합니다. 
1. **개요** 창에서 **대량 등록**을 선택합니다.  

   ![대량 등록을 선택하여 SQL Server의 여러 인스턴스를 등록](media/sql-server-extended-security-updates/bulk-register-sql-server-instances.png)

1. 파일 아이콘을 선택하여 .CSV 파일 위치로 이동합니다. .CSV 파일을 선택합니다. 그런 다음 **등록**을 선택하여 파일을 업로드하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 여러 인스턴스를 등록합니다. 

   ![CSV 파일을 업로드하여 SQL Server의 여러 인스턴스를 등록](media/sql-server-extended-security-updates/upload-csv-file-for-bulk-registration.png)

### <a name="formatting-requirements-for-csv-file"></a>CSV 파일에 대한 서식 지정 요구 사항
- 값은 쉼표로 구분됩니다.
- 값이 작은따옴표나 큰따옴표가 아닙니다.
- 열 이름은 대/소문자를 구분하지 않지만 아래와 같이 **명명**되어야 합니다. 
  - name
  - 버전
  - edition
  - cores
  - hostType
  - subscriptionID<sup>1</sup>
  - resourceGroup<sup>1</sup>
  - azureVmName<sup>1</sup>
  - AzureVmOS<sup>1</sup>

<sup>1</sup> Azure Virtual Machines에만 필요합니다. 

#### <a name="csv-example-1---on-premises"></a>CSV 예제 1 - 온-프레미스

온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 CSV 파일은 다음과 같습니다. 

```csv
name,version,edition,cores,hostType
Server1\SQL2008,2008,Enterprise,12,Physical Server
Server1\SQL2008R2,2008 R2,Enterprise,12,Physical Server
Server2\SQL2008R2,2008 R2,Enterprise,24,Physical Server
Server3\SQL2008R2,2008 R2,Enterprise,12,Virtual Machine
Server4\SQL2008,2008,Developer,8,Physical Server  
```

CSV 파일 예제는 [MyPhysicalServers.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyPhysicalServers.csv)를 참조하세요.

#### <a name="csv-example-2---azure-vm"></a>CSV 예제 2 - Azure VM

Azure Virtual Machine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 CSV 파일은 다음과 같습니다. 

```csv
name,version,edition,cores,hostType,subscriptionId,resourceGroup,azureVmName,azureVmOS    
ProdServerUS1\SQL01,2008 R2,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ProdServerUS1\SQL02,2008 R2,Enterprise,24,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM1,2012    
ServerUS2\SQL01,2008,Enterprise,12,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
ServerUS2\SQL02,2008,Enterprise,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM2,2012 R2    
SalesServer\SQLProdSales,2008 R2,Developer,8,Azure Virtual Machine,61868ab8-16d4-44ec-a9ff-f35d05922847,RG,VM3,2008 R2  
```

Azure VM 대상 CSV 파일 예제는 [MyAzureVMs.csv](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts/MyAzureVMs.csv)를 참조하세요. 


> [!TIP]
> .CSV 파일에 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 등록 정보를 생성할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 PowerShell 예제 스크립트는 [ESU 등록 스크립트 예제](https://github.com/microsoft/sql-server-samples/blob/master/samples/manage/sql-server-extended-security-updates/scripts.md)를 참조하세요. 

## <a name="download-esus"></a>ESU 다운로드

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 SQL Server 레지스트리 서비스에 등록한 후에는 Azure Portal에서 찾은 링크를 사용하여 연장 보안 업데이트 패키지를 다운로드할 수 있습니다(사용 가능해진 경우). 

ESU를 다운로드하려면 다음 단계를 수행합니다. 

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. 
1. **SQL Server 레지스트리** 리소스로 이동합니다. 
1. 탐색 창에서 **보안 업데이트**를 선택합니다. 

   ![사용 가능한 업데이트에 대한 보안 업데이트 창 확인](media/sql-server-extended-security-updates/security-updates-sql-registry.png)

1. 사용할 수 있게 되면 여기에서 보안 업데이트를 다운로드합니다. 

## <a name="faq"></a>FAQ

연장 보안 업데이트에 대한 일반적인 질문과 대답은 [연장 보안 업데이트 FAQ](https://www.microsoft.com/cloud-platform/extended-security-updates)에서 찾을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 FAQ는 다음과 같습니다. 

**SQL Server 2008 및 2008 R2에 대한 지원이 종료되는 시기는 언제입니까?**

[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 대한 지원 종료 날짜는 2019년 7월 9일입니다. 

**지원 종료는 무엇을 의미하나요?**

Microsoft 수명 주기 정책은 비즈니스 및 개발자 제품(예: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows Server)에 대해 10년간의 지원(일반 지원 5년, 연장 지원 5년)을 제공합니다. 정책에 따라, 연장 지원 기간이 종료된 후에는 패치 또는 보안 업데이트가 없으므로 이로 인해 보안 및 규정 준수 문제가 발생하고 고객의 애플리케이션 및 비즈니스가 심각한 보안 위험에 노출될 수 있습니다.

**연장 보안 업데이트에 적합한 SQL Server 버전은 무엇인가요?**

[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]의 Enterprise, Datacenter, Standard, Web 및 Workgroup Edition은 x86 및 x64 버전 모두 연장 보안 업데이트에 적합합니다. 

**연장 보안 업데이트 제품은 언제 사용할 수 있나요?**

이제 연장 보안 업데이트를 구매할 수 있으며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 라이선스 파트너에서 주문할 수 있습니다. 연장 보안 업데이트 제공은 지원 종료 날짜 이후 시작됩니다(사용 가능한 경우). Azure로 마이그레이션하는 데 관심이 있는 고객은 바로 시작할 수 있습니다. 

**연장 보안 업데이트에는 무엇이 포함되나요?** 

연장 보안 업데이트에는 2019년 7월 9일 이후 [Microsoft 보안 응답 센터(MSRC)](https://portal.msrc.microsoft.com/)에 의해 **중요**로 평가된 보안 업데이트 및 공지의 프로비전이 포함됩니다. 사용 가능해지면 연장 보안 업데이트가 배포됩니다. 연장 보안 업데이트에는 기술 지원이 포함되지 않지만 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 계획을 사용하여 연장 보안 업데이트가 적용되는 워크로드에 대한 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 질문에 대한 지원을 받을 수 있습니다. 연장 보안 업데이트에는 새로운 기능, 기능 향상 또는 고객이 요청한 수정 사항이 포함되지 않습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 필요한 것으로 간주되는 비보안 픽스를 포함할 수 있습니다.

**SQL Server 2008 및 2008 R2에 대한 연장 보안 업데이트가 "중요" 업데이트만 제공하는 이유는 무엇입니까?**

과거의 지원 종료 이벤트에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 엔터프라이즈 고객의 규정 준수 기준을 충족하는 중요 보안 업데이트만 제공했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 일반적인 월간 보안 업데이트를 제공하지 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 영향을 받는 제품으로 식별된 MSRC 게시판에 대해 주문형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 업데이트(GDR)만 제공합니다.
MSRC가 중요로 평가하지 않아 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 중요 업데이트를 제공되지 않지만 고객은 중요한 것으로 간주하는 상황에서는 사례별로 고객과 협력하여 적절한 완화 방법을 제안할 것입니다.

**연장 보안 업데이트에 적격한 라이선스 프로그램은 무엇인가요?**

소프트웨어 보증 고객은 EA(기업계약), EAS(기업 정기가입 계약), SCE(서버 및 클라우드 등록) 또는 EES(교육 솔루션 등록)에서 온-프레미스로 연장 보안 업데이트를 구매할 수 있습니다. 소프트웨어 보증이 동일한 등록에 있지 않아도 됩니다.

**연장 보안 업데이트를 활용하려면 SQL Server 고객이 최신 서비스 팩을 실행해야 합니까?**

예, 고객이 연장 보안 업데이트를 적용하려면 최신 서비스 팩과 함께 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows Server 2008 및 2008 R2를 실행해야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 최신 서비스 팩에 적용될 수 있는 업데이트만 생성합니다.

**소프트웨어 보증이 없는 SQL Server 고객을 위한 옵션은 무엇인가요?** 

소프트웨어 보증이 없는 고객의 경우 연장 보안 업데이트에 액세스할 수 있는 대체 옵션은 Azure로 마이그레이션하는 것입니다. 가변 워크로드의 경우 고객은 언제든지 규모를 확장하거나 축소할 수 있는 종량제를 통해 Azure로 마이그레이션하는 것이 좋습니다. 예측 가능한 워크로드의 경우 고객은 서버 구독 및 예약 인스턴스를 통해 Azure로 마이그레이션하는 것이 좋습니다.
  
**이 제품은 SQL Server 2005에도 적용되나요?**

아니요. 이러한 이전 버전의 경우 최신 버전으로 업그레이드하는 것이 좋지만 고객이 이 서비스를 활용하려면 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 버전으로 업그레이드할 수 있습니다.

**Azure에 새 SQL Server 2008 또는 2008 R2 인스턴스를 배포하고 연장 보안 업데이트를 계속 받을 수 있나요?**

예, 고객은 Azure 가상 머신에서 새 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 인스턴스를 시작하고 연장 보안 업데이트에 액세스할 수 있습니다.

**연장 보안 업데이트를 구매하지 않고 지원 종료 날짜 이후에 SQL Server 2008 또는 2008 R2에 대한 기술 지원을 온-프레미스에서 받을 수 있나요?**

아니요. 고객이 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]를 사용하고 연장 보안 업데이트 없이 마이그레이션하는 동안 온-프레미스로 유지하도록 선택하는 경우 지원 계획을 보유한 경우에도 지원 티켓을 기록할 수 없습니다. 그러나 Azure로 마이그레이션하는 경우 Azure 지원 계획을 사용하여 지원을 받을 수 있습니다.

**SQL Server 2008 및 2008 R2 고객이 자신의 라이선스(BYOL)를 사용하려는 경우 소프트웨어 보증 범위를 유지해야 하나요?**

예, 고객은 라이선스 이동 프로그램의 일부로 Azure Virtual Machines에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 BYOL 프로그램을 활용하려면 소프트웨어 보증이 필요합니다. 소프트웨어 보증이 없는 고객의 경우 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 환경의 Azure SQL Database Managed Instance로 이동하는 것이 좋습니다. 고객은 종량제 Azure Virtual Machines로 마이그레이션할 수도 있습니다. 또한 SQL by core 라이선스를 사용하는 소프트웨어 보증 고객은 AHB(Azure 하이브리드 혜택)를 사용하여 Azure로 마이그레이션할 수도 있습니다.

Azure SQL Database Managed Instance는 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 거의 100% 호환성을 제공하는 Azure 서비스입니다. Managed Instance는 기본 제공되는 고가용성/재해 복구 기능과 지능형 성능 기능을 제공하고 즉석에서 크기를 조정하는 기능을 제공합니다. 또한 Managed Instance는 수동 보안 패치 및 업그레이드가 필요 없는 무버전 환경을 제공합니다. BYOL 프로그램에 대한 자세한 내용은 Azure 가격 책정 가이드 페이지를 참조하세요.

**고객이 Azure에서 SQL Server를 실행하는 데 필요한 옵션은 무엇인가요?**

고객은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경을 "무버전" 옵션을 제공하는 완전히 관리되는 데이터 플랫폼 서비스(PaaS)인 Azure SQL Database Managed Instance로 이동하여 지원 종료 날짜와 관련된 문제를 제거하거나, Azure Virtual Machines 보안 업데이트에 액세스할 수 있습니다. 마이그레이션된 데이터베이스는 레거시 시스템과의 호환성을 유지합니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

연장 보안 업데이트는 지원 종료 날짜인 2019년 7월 9일 이후 3년 동안 Azure Virtual Machines에서 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 사용할 수 있습니다. [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에서 업그레이드하려는 고객의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 후속 버전이 지원됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]까지 고객은 지원되는 최신 서비스 팩에 있어야 합니다. [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 고객은 최신 누적 업데이트를 사용하는 것이 좋습니다. 서비스 팩은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 사용할 수 없으며, 누적 업데이트 및 GDR(일반 배포 릴리스)만 사용할 수 있습니다.

Azure SQL Database Managed Instance는 가장 광범위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진 호환성 및 기본 VNET(가상 네트워크) 지원을 제공하는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 인스턴스 범위 배포 옵션이므로 앱을 변경하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 Managed Instance로 마이그레이션할 수 있습니다. 풍부한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 노출 영역을 완전히 관리되는 지능형 서비스의 운영 및 금융 혜택과 결합합니다. 새 Azure Database Migration Service를 활용하여 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]를 애플리케이션 코드 변경이 거의 또는 전혀 없이 Azure SQL Database Managed Instance로 이동할 수 있습니다.

**고객이 SQL Server 2008 및 2008 R2 버전에 대한 Azure 하이브리드 혜택을 활용할 수 있나요?**

예, 활성 소프트웨어 보증 또는 동등한 서버 구독이 있는 고객은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 Azure Virtual Machines에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 할인 가격의 기존 온-프레미스 라이선스 투자를 사용하여 Azure 하이브리드 혜택을 활용할 수 있습니다.

**고객이 Azure Government 지역에서 무료로 연장 보안 업데이트를 받을 수 있나요?**

예, Azure Government 지역의 Azure Virtual Machines에서 연장 보안 업데이트를 사용할 수 있습니다.

**고객이 Azure Stack에서 연장 보안 업데이트를 무료로 이용할 수 있나요?**

예, 고객은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 Windows Server 2008 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]를 Azure Stack으로 마이그레이션하고, 지원 종료 날짜 이후 추가 비용 없이 연장 보안 업데이트를 받을 수 있습니다.

**공유 스토리지를 사용하는 2008 및 2008 R2 SQL 클러스터 고객의 경우 Azure로 마이그레이션하기 위한 지침은 무엇인가요?**

Azure는 현재 공유 스토리지 클러스터링을 지원하지 않습니다. Azure에서 고가용성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 구성하는 방법에 대한 지침은 [SQL Server 고가용성 가이드](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)를 참조하세요.

**고객이 타사가 호스트하는 SQL Server에서 연장 보안 업데이트를 활용할 수 있나요?**

고객은 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 환경을 다른 클라우드 공급자의 PaaS 구현으로 이동하는 경우 연장 보안 업데이트를 활용할 수 없습니다. 고객이 가상 머신(IaaS)으로 이동하려는 경우 소프트웨어 보증을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 라이선스 이동으로 활용하여 마이그레이션하고, [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 연장 보안 업데이트를 구입하여 인증된 SPLA 호스터의 서버에 있는 VM(IaaS)에서 실행되는 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 인스턴스에 패치를 수동으로 적용할 수 있습니다. 그러나 Azure에서의 무료 업데이트가 더 매력적인 제품입니다.

**Azure 가상 머신에서 SQL Server의 성능을 향상시키기 위한 모범 사례는 무엇인가요?** 

Azure 가상 머신에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능을 최적화하는 방법에 대한 지침은 [SQL Server 최적화 가이드](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)를 참조하세요. 

## <a name="see-also"></a>참고 항목

- [SQL Server 2008/2008 R2 수명 주기 페이지](https://support.microsoft.com/lifecycle/search?alpha=sql%20server%202008)
- [SQL Server 2008/2008 R2 지원 종료 페이지](https://aka.ms/sqleos)
- [연장 보안 업데이트 FAQ(질문과 대답)](https://aka.ms/sqleosfaq)
- [Microsoft 보안 응답 센터(MSRC)](https://portal.msrc.microsoft.com/security-guidance/summary)
- [Azure Automation을 사용하여 Windows 업데이트 관리](/azure/automation/automation-tutorial-update-management)
- [SQL Server VM 자동화된 패치 적용](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)
- [Microsoft 데이터 마이그레이션 가이드](https://datamigration.microsoft.com/)
- [Azure 마이그레이션: 현재 SQL Server 2008/2008 R2를 Azure VM으로 이동하는 리프트 앤 시프트 옵션](https://azure.microsoft.com/services/azure-migrate/)
- [SQL 마이그레이션을 위한 클라우드 채택 프레임 워크](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)
- [GitHub의 ESU 관련 스크립트](https://github.com/microsoft/sql-server-samples/tree/master/samples/manage/sql-server-extended-security-updates/scripts)

