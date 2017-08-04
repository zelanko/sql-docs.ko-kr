---
title: "데이터 스트리밍 대상 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e95b4d887bea5783be935a40877d590b8e8dcff
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="data-streaming-destination"></a>데이터 스트리밍 대상
  **데이터 스트리밍 대상[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]은 **SSIS용 OLE DB 공급자**가 SSIS 패키지의 출력을 탭 형식의 결과 집합으로 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** (SSIS) 대상 구성 요소입니다. SSIS용 OLE DB 공급자를 사용하는 연결 서버를 만든 다음 연결 서버에 SQL 쿼리를 실행하여 SSIS 패키지에서 반환한 데이터를 표시할 수 있습니다.  
  
 다음 예제의 쿼리는 SSIS 카탈로그 Power BI 폴더에 있는 SSISPackagePublishing 프로젝트의 Package.dtsx 패키지에서 출력을 반환합니다. 이 쿼리는 연결된 서버 이름[Integration Services의 기본 연결 서버]을 사용하며, 이 이름은 새로운 SSIS용 OLE DB 공급자를 사용합니다. 쿼리에는 SSIS 카탈로그의 폴더 이름, 프로젝트 이름, 패키지 이름이 포함됩니다. SSIS용 OLE DB 공급자는 쿼리에 지정된 패키지를 실행하고 탭 형식의 결과 집합을 반환합니다.  
  
```  
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
>  자세한 단계는 [연습: SSIS 패키지를 SQL 뷰로 게시](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)를 참조하세요.  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>Power BI 관리 센터를 사용하여 SSIS 패키지의 출력 데이터를 OData 피드로 표시  
 IT 관리자는 Power BI 관리 센터를 사용하여 온-프레미스 데이터 원본의 데이터를 사용자에게 OData 피드로 표시할 수 있습니다. Power BI 관리 센터에서는 기본적으로 SQL Server 데이터 원본만 등록할 수 있습니다. 하지만 **데이터 스트리밍 대상** 과 **SQL Server Integration Services(SSISOLEDB)용 Microsoft OLE DB 공급자** 를 사용하면 SSIS 패키지를 데이터 원본으로 등록하고 SSIS 패키지의 결과 데이터를 사용자에게 OData 피드로 표시할 수 있습니다.  
  
 관리 센터를 사용하면 SQL Server 데이터베이스에 뷰를 게시할 수 있습니다. 따라서 SSIS 패키지 게시 마법사를 사용하여 SSIS 패키지를 SQL 뷰로 게시할 수 있습니다. 그런 다음 Power BI 관리 센터의 OData 피드에 포함할 뷰를 선택할 수 있습니다. 데이터 관리자는 Excel용 파워 쿼리 추가 기능을 사용하여 SSIS 패키지의 피드를 사용할 수 있습니다.  
  
 자세한 연습은 [SSIS 패키지를 OData 피드 원본으로 게시](http://go.microsoft.com/fwlink/?LinkID=317367)를 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [연습: SSIS 패키지를 SQL 뷰로 게시](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [데이터 스트리밍 대상 구성](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SSIS 패키지를 OData 피드 원본으로 게시](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
