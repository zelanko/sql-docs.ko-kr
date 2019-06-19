---
title: 데이터 스트리밍 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 504c05882d1e7c690b8ddbd46c331073f63bbb7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726999"
---
# <a name="data-streaming-destination"></a>데이터 스트리밍 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **데이터 스트리밍 대상[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]은**SSIS용 OLE DB 공급자**가 SSIS 패키지의 출력을 탭 형식의 결과 집합으로 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** (SSIS) 대상 구성 요소입니다. SSIS용 OLE DB 공급자를 사용하는 연결 서버를 만든 다음 연결 서버에 SQL 쿼리를 실행하여 SSIS 패키지에서 반환한 데이터를 표시할 수 있습니다.  
  
 다음 예제의 쿼리는 SSIS 카탈로그 Power BI 폴더에 있는 SSISPackagePublishing 프로젝트의 Package.dtsx 패키지에서 출력을 반환합니다. 이 쿼리는 연결된 서버 이름[Integration Services의 기본 연결 서버]을 사용하며, 이 이름은 새로운 SSIS용 OLE DB 공급자를 사용합니다. 쿼리에는 SSIS 카탈로그의 폴더 이름, 프로젝트 이름, 패키지 이름이 포함됩니다. SSIS용 OLE DB 공급자는 쿼리에 지정된 패키지를 실행하고 탭 형식의 결과 집합을 반환합니다.  
  
```sql
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>데이터 피드 게시 구성 요소  
 데이터 피드 게시 구성 요소는 SSIS용 OLE DB 공급자, 데이터 스트리밍 대상, SSIS 패키지 게시 마법사가 있습니다. 이 마법사를 사용하면 SSIS 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 인스턴스의 SQL 뷰로 게시할 수 있습니다. 이 마법사는 연결된 서버의 쿼리를 나타내는 SQL 뷰와 SSIS용 OLE DB 공급자를 사용하는 연결 서버를 만드는 과정을 도와줍니다. SSIS 패키지의 쿼리 결과를 탭 형식의 데이터 집합으로 표시하는 뷰를 실행합니다.  
  
 SSISOLEDB 공급자가 설치되어 있는지 확인하려면 SQL Server Management Studio에서 **서버 개체**, **연결된 서버**, **공급자**를 확장한 다음 **SSISOLEDB** 공급자가 표시되는지 확인합니다. **SSISOLEDB**를 두 번 클릭하고 **Inprocess 허용** 을 사용하도록 설정한 다음(설정되지 않은 경우) **확인**을 클릭합니다.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>SSIS 패키지를 SQL 뷰로 게시  
 다음 절차는 SSIS 패키지를 SQL 뷰로 게시하는 단계에 대해 설명합니다.  
  
1.  **데이터 스트리밍 대상** 구성 요소를 사용하여 SSIS 패키지를 만들고 이 패키지를 SSIS 카탈로그에 배포합니다.  
  
2.  ISDataFeedPublishingWizard.exe from C:\Program Files\Microsoft SQL Server\130\DTS\Binn을 실행하거나 시작 메뉴에서 데이터 피드 게시 마법사를 실행하여 **SSIS 패키지 게시 마법사** 를 실행합니다.  
  
     이 마법사는 SSIS용 OLE DB 공급자(SSISOLEDB)를 사용하여 연결된 서버를 만든 다음 연결된 서버에 대한 쿼리로 구성된 SQL 뷰를 만듭니다. 이 쿼리에는 SSIS 카탈로그의 폴더 이름, 프로젝트 이름, 패키지 이름이 포함됩니다.  
  
3.  SQL Server Management Studio에서 SQL 뷰를 실행하고 SSIS 패키지의 결과를 검토합니다. 이 뷰는 사용자가 만든 연결 서버를 통해 SSIS용 OLE DB 공급자에게 쿼리를 전송합니다. SSIS용 OLE DB 공급자는 쿼리에 지정된 패키지를 실행하고 탭 형식의 결과 집합을 반환합니다.  
  
> [!IMPORTANT]  
>  자세한 단계에 대해서는 [연습: SSIS 패키지를 SQL 뷰로 게시](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)를 참조하세요.  

## <a name="configure-data-streaming-destination"></a>데이터 스트리밍 대상 구성
  **고급 데이터 스트리밍 대상 편집기** 대화 상자를 사용하여 데이터 스트리밍 대상을 구성합니다. 구성 요소를 두 번 클릭하거나 데이터 흐름 디자이너에서 구성 요소를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭하여 이 대화 상자를 엽니다.  
  
 이 대화 상자에는 **구성 요소 속성**, **입력 열**, **입력 및 출력 속성**, 이렇게 3개 탭이 있습니다.  
  
## <a name="component-properties-tab"></a>구성 요소 속성 탭  
 이 탭에는 다음과 같은 편집 가능 필드가 있습니다.  
  
|필드|설명|  
|-----------|-----------------|  
|속성|패키지에 포함된 데이터 스트리밍 대상 구성 요소의 이름입니다.|  
|ValidateExternalMetadata|디자인 타임에 외부 데이터 원본을 사용하여 구성 요소의 유효성을 검사하는지 여부를 나타냅니다. false로 설정하면 외부 데이터 원본에 대한 유효성 검사가 런타임까지 연기됩니다.|  
|IDColumnName|데이터 피드 게시 마법사가 생성한 뷰에는 이 추가 ID 열이 있습니다. 다른 애플리케이션이 데이터를 OData 피드로 사용할 때 ID 열은 데이터 흐름의 출력 데이터에 대한 EntityKey로 사용됩니다.<br /><br /> 이 열의 기본값은 _ID입니다. ID 열에 대해 다른 이름을 지정할 수 있습니다.|  
  
## <a name="input-columns-tab"></a>입력 열 탭  
 이 탭의 위쪽 창에는 사용 가능한 모든 입력 열이 표시됩니다. 입력 열 중에서 이 구성 요소의 출력에 포함할 열을 선택합니다. 선택한 열은 아래쪽 창의 목록에 표시됩니다. 목록에서 **출력 별칭** 필드에 대한 새 이름을 입력해 출력 열의 이름을 변경할 수 있습니다.  
  
## <a name="input-output-properties-tab"></a>입력 및 출력 속성 탭  
 이 탭에서는 입력 열 탭에서와 비슷한 방식으로 출력 열의 이름을 변경할 수 있습니다. 왼쪽 트리 뷰에서 **데이터 스트리밍 대상 입력** 과 **입력 열**을 차례로 확장합니다. 입력 열 이름을 클릭하고 오른쪽 창에서 출력 열 이름을 변경합니다.
