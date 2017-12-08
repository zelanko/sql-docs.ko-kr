---
title: "파티션 병합 cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 15c7b069-897d-4bc8-a808-59cbeeabe4d8
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 702efef3e86e8200d80c47fe6367b186afad081e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="merge-partition-cmdlet"></a>Merge-Partition cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합한 다음 원본 파티션을 삭제합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Merge-Partition cmdlet은 하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합한 다음 원본 파티션을 삭제합니다. 다음 조건이 모두 충족되는 경우에만 파티션을 병합할 수 있습니다.  
  
-   파티션이 같은 측정값 그룹에 있어야 합니다.  
  
-   파티션이 같은 컴퓨터에 있어야 합니다.  
  
-   파티션이 같은 저장 모드(MOLAP, HOLAP 및 다차원 데이터베이스의 경우 ROLAP)를 공유해야 합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-name-string"></a>-이름 \<문자열 >  
 원본 파티션 데이터를 병합할 대상 파티션을 지정합니다. 이 파티션은 이미 있어야 합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-sourcepartition-string"></a>-SourcePartition \<문자열 >  
 대상 파티션에 병합될 원본 파티션을 지정합니다. 병합할 파티션의 쉼표로 구분된 목록을 만들 수 있습니다. 변수를 사용하여 목록을 저장합니다. 예를 들어 $Sources="Sales_2008", "Sales_2009", "Sales_2010"을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-database-string"></a>-데이터베이스 \<문자열 >  
 파티션이 속한 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-cube-string"></a>-큐브 \<문자열 >  
 파티션이 속한 큐브를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-measuregroup-string"></a>-MeasureGroup \<문자열 >  
 파티션이 속한 측정값 그룹을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-server-string"></a>-서버 \<문자열 >  
 cmdlet이 연결하고 실행할 Analysis Services 인스턴스를 지정합니다. 서버 이름을 제공하지 않으면 localhost에 연결됩니다. 기본 인스턴스의 경우에는 서버 이름만 지정합니다. 명명된 인스턴스의 경우에는 servername\instancename 형식을 사용합니다. HTTP 연결의 경우 http[s]://server[:port]/virtualdirectory/msmdpump.dll 형식을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|localhost|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 이 매개 변수는 HTTP 액세스를 사용하도록 구성한 Analysis Service 인스턴스에 대해 HTTP 연결을 사용할 때 사용자 이름 및 암호를 전달하는 데 사용됩니다. 자세한 내용은 참조 [HTTP 액세스 구성 Analysis Services 인터넷 정보 서비스 &#40; IIS &#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) HTTP 연결에 대 한 합니다.  
  
 이 매개 변수를 지정하면 사용자 이름 및 암호를 사용하여 지정된 Analysis Server 인스턴스에 연결합니다. 자격 증명을 지정하지 않으면 도구를 실행 중인 사용자의 기본 Windows 계정이 사용됩니다.  
  
 이 매개 변수를 사용하려면 먼저 Get-Credential을 사용하여 PSCredential 개체를 만들어 사용자 이름 및 암호를 지정합니다(예: `$Cred=Get-Credential “adventure-works\bobh”`). 그런 다음 이 개체를 –Credential 매개 변수에 파이프할 수 있습니다 `(-Credential:$Cred`).  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByValue)|  
|와일드카드 문자 허용|false|  
  
### <a name="-targetpartition-microsoftanalysisservicespartition"></a>-TargetPartition \<Microsoft.AnalysisServices.Partition >  
 원본 파티션을 병합할 대상 파티션을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|System.string|  
|출력|InclusionThresholdSetting|  
  
## <a name="example-1"></a>예제 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 이 명령은 2001, 2002, 2003의 파티션을 2004에 대한 파티션에 병합한 다음 이전 연도의 파티션을 삭제합니다.  
  

  
