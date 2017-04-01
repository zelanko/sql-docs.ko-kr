---
title: "Analysis Services 설치 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Analysis Services 설치
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 은(는) 보고서, 스프레드시트 및 대시보드에서 액세스할 수 있는 테이블 형식 모델, 다차원 큐브 및 데이터 마이닝 모델을 호스팅하는 분석 데이터베이스 서버입니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 다중 인스턴스로 한 컴퓨터에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 사본을 여러 개 설치하거나 신규 버전과 기존 버전을 함께 실행할 수 있습니다. 설치한 모든 인스턴스는 설치 도중 결정된 세 가지 모드(다차원 및 데이터 마이닝, 테이블 형식 또는 SharePoint) 중 하나로 실행됩니다. 다중 모드를 사용하려면 각 모드에 대한 별도의 인스턴스가 필요합니다.  
  
 특정 모드에 서버를 설치한 이후에는 해당 모드를 준수하는 호스트 솔루션으로 사용할 수 있습니다. 예를 들어, 네트워크를 통해 테이블 형식 모델 데이터에 액세스하려는 경우 테이블 형식 모드 서버가 필요합니다.  
  
## 도구 및 디자이너 다운로드  
 SQL Server 설치 프로그램은 솔루션 설계 또는 서버 관리를 위해 사용되는 모델 디자이너 또는 관리 도구를 더 이상 설치하지 않습니다. 이 릴리스에서 도구는 별도로 설치되고 다음 링크에서 다운로드할 수 있습니다.  
  
-   [SQL Server 2016용 SQL Server Management Studio 다운로드](https://msdn.microsoft.com/en-US/library/mt238290.aspx)  
  
-   [SQL Server 2016용 SQL Server Data Tools 다운로드](https://msdn.microsoft.com/en-US/library/mt204009.aspx)  
  
 Analysis Services 인스턴스 및 데이터로 작업하려면 Management Studio와 SQL Server Data Tools가 모두 있어야 합니다. 도구는 어디에나 설치할 수 있지만 서버에서 포트를 구성한 후에 연결해야 합니다. 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 를 참조하세요.  
  
## 마법사를 사용한 설치  
 다음 목록에서는 Analysis Services를 설치하는 데 사용되는 SQL Server 설치 마법사의 해당 페이지를 보여 줍니다.  
  
1.  설치 프로그램의 기능 트리에서 **Analysis Services** 를 선택합니다.  
  
     ![Setup feature tree showing Analsyis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "Setup feature tree showing Analsyis Services")  
  
2.  테이블 형식 인스턴스를 사용하려는 경우 Analysis Services 구성 페이지에서 **테이블 형식 모드** 를 선택해야 합니다. 그렇지 않은 경우 기본으로 **다차원 및 데이터 마이닝 모드**가 선택됩니다.  
  
     ![Setup page with Analysis Services config options](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "Setup page with Analysis Services config options")  
  
 다차원 및 데이터 마이닝 모드는 모델이 Analysis Services에 배포되는 기본 저장소로 MOLAP를 사용합니다. 쿼리 데이터를 Analysis Services 다차원 데이터베이스에 저장하지 않고 쿼리를 관계형 데이터베이스에서 직접 실행하려면 서버에 배포한 후 솔루션이 ROLAP를 사용하도록 구성합니다.  
  
 테이블 형식 모드는 xVelocity 메모리 내 분석 엔진(VertiPaq)을 사용합니다. 이 엔진은 Analysis Services에 배포하는 테이블 형식 모델에 대한 기본 저장소입니다. 테이블 형식 모델 솔루션을 서버에 배포한 이후에 테이블 형식 솔루션을 선택적으로 구성하여 메모리 집중형 저장소 대신에 DirectQuery 디스크 저장소를 사용할 수 있습니다.  
  
 기본이 아닌 저장소 모드를 사용하는 경우 성능을 향상하기 위해 메모리 관리 및 IO 설정을 조정할 수 있습니다. 자세한 내용은 [Analysis Services의 서버 속성](../../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
## 명령줄 설치  
 SQL Server 설치에는 서버 모드를 지정하는 매개 변수(**ASSERVERMODE**)가 포함됩니다. 다음 예에서는 테이블 형식 서버 모드에 Analysis Services를 설치하는 명령줄 설치를 보여 줍니다.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** 은 17자 미만이어야 합니다.  
  
 모든 자리 표시자 계정 값을 유효한 계정 및 암호로 바꾸어야 합니다.  
  
 **ASSERVERMODE**는 대/소문자를 구분합니다.  모든 값은 대문자로 표시해야 합니다. 다음 표에는 **ASSERVERMODE**의 유효한 값에 대한 설명이 나와 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|이 값은 기본값입니다. **ASSERVERMODE**를 설정하지 않은 경우 서버는 다차원 서버 모드에 설치됩니다.|  
|POWERPIVOT| 이 값은 선택 사항입니다.  실제로 **ROLE** 매개 변수를 설정한 경우 서버 모드는 자동으로 1로 설정되며 **ASSERVERMODE**를 SharePoint용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 설치에 대한 옵션으로 만듭니다. 자세한 내용은 [명령 프롬프트에서 Power Pivot 설치](http://msdn.microsoft.com/ko-kr/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)를 참조하십시오.|  
|TABULAR|명령줄 설치를 사용하여 테이블 형식 모드에 Analysis Services를 설치하는 경우 이 값이 필요합니다.|  
  
## 참고 항목  
 [Analysis Services 인스턴스의 서버 모드 확인](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [메모리 내 테이블 형식 데이터베이스를 SSMS&#40;SQL Server Management Studio&#41;의 DirectQuery로 변환](../Topic/Convert%20an%20in-memory%20Tabular%20Database%20to%20DirectQuery%20in%20SQL%20Server%20Management%20Studio%20\(SSMS\).md)   
 [테이블 형식 모델링&#40;SSAS&#41;](../Topic/Tabular%20Modeling%20\(SSAS\).md)  
  
  