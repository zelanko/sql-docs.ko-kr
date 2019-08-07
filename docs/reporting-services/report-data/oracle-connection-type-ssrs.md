---
title: Oracle 연결 형식 (SSRS, Power BI Report Server 및 보고서 작성기) | Microsoft Docs
ms.date: 07/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2942ad1432b2674ab0b9906b5ab6e2f07be83ae7
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632079"
---
# <a name="oracle-connection-type-ssrs-power-bi-report-server-and-report-builder"></a>Oracle 연결 형식 (SSRS, Power BI Report Server 및 보고서 작성기)

보고서에서 Oracle 데이터베이스의 데이터를 사용하려면 Oracle 유형의 보고서 데이터 원본을 기반으로 하는 데이터 세트가 있어야 합니다. 이 기본 제공 데이터 원본 유형은 Oracle Data Provider를 사용하며 Oracle 클라이언트 소프트웨어 구성 요소를 필요로 합니다. 이 문서에서는 Reporting Services, Power BI Report Server 및 보고서 작성기에 대 한 드라이버를 다운로드 하 고 설치 하는 방법을 설명 합니다.

## <a name="64-bit-drivers-for-the-report-servers"></a>보고서 서버용 64 비트 드라이버

Power BI Report Server 및 SQL Server Reporting Services 2016 및 2017는 모두 관리 되는 ODP.NET을 사용 합니다. 다음 단계는 최신 18x 드라이버를 사용 하는 경우에만 필요 합니다. C:\oracle64.에 파일을 설치 했다고 가정 합니다.

1. Oracle 다운로드 사이트에서 [oracle 64-BIT ODAC Oracle Universal Installer (oua)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html)를 설치 합니다. 
2. ODP.NET 관리 클라이언트를 GAC: C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/action: gac/providerpath: C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll에 등록 합니다.
3. ODP.NET 관리 되는 클라이언트 항목을 machine.config에 추가: C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/action: config/force/제품: odpm/frameworkversion: v 4.0.30319/productversion: 4.122.18.3

## <a name="32-bit-drivers-for-report-builder"></a>보고서 작성기에 대 한 32 비트 드라이버
다음 단계는 최신 18x 드라이버를 사용 하는 경우에만 필요 합니다. C:\oracle32.에 파일을 설치 했다고 가정 합니다.

1. Oracle 다운로드 사이트에서 [oracle 32-BIT ODAC Oracle Universal Installer (oua)](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html)를 설치 합니다.
2. ODP.NET 관리 클라이언트를 GAC: C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/action: gac/providerpath: C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll에 등록 합니다.
3. ODP.NET 관리 되는 클라이언트 항목을 machine.config에 추가: C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe/action: config/force/제품: odpm/frameworkversion: v 4.0.30319/productversion: 4.122.18.3

 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Connection"></a> 연결 문자열  
 데이터 원본 연결에 사용할 자격 증명 및 연결 정보는 데이터베이스 관리자에게 문의하십시오. 다음 연결 문자열 예에서는 유니코드를 사용하는 "Oracle18"이라는 서버의 Oracle 데이터베이스를 지정합니다. 서버 이름은 Tnsnames.ora 구성 파일에 Oracle 서버 인스턴스 이름으로 정의되어 있는 이름과 일치해야 합니다.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 연결 문자열 예제는 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
  
##  <a name="Query"></a> 쿼리  
 데이터 세트를 만들려면 드롭다운 목록에서 저장 프로시저를 선택하거나 SQL 쿼리를 만듭니다. 쿼리를 만들려면 텍스트 기반 쿼리 디자이너를 사용해야 합니다. 자세한 내용은 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
 결과 집합을 하나만 반환하는 저장 프로시저를 지정할 수 있습니다. 커서 기반 쿼리는 사용할 수 없습니다.  
  
##  <a name="Parameters"></a> 매개 변수  
 쿼리에 쿼리 변수가 포함된 경우 해당 보고서 매개 변수가 자동으로 생성됩니다. 이 확장 프로그램은 명명된 매개 변수를 지원합니다. Oracle 버전 9 이상의 경우 다중값 매개 변수가 지원됩니다.  
  
 보고서 매개 변수는 수정해야 할 수도 있는 기본 속성 값을 사용하여 만들어집니다. 예를 들어 각 보고서 매개 변수의 데이터 형식은 **Text**입니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)유형의 보고서 데이터 원본을 기반으로 하는 데이터 집합이 있어야 합니다.  
  
  
##  <a name="Remarks"></a> 주의  
 Oracle 데이터 원본을 연결하려면 시스템 관리자가 Oracle 데이터베이스에서 데이터를 검색할 수 있도록 하는 .NET Data Provider for Oracle 버전을 설치해야 합니다. 이 데이터 공급자는 보고서 작성기와 동일한 컴퓨터뿐 아니라 보고서 서버에도 설치되어야 합니다.  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Reporting Services를 사용한 Oracle 데이터 원본 구성 및 액세스 방법](https://support.microsoft.com/kb/834305)  
-   [NETWORK SERVICE 보안 주체에 대한 사용 권한을 추가하는 방법](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>대체 데이터 확장 프로그램 
 
 OLE DB 데이터 원본 유형을 사용하여 Oracle 데이터베이스에서 데이터를 검색할 수도 있습니다. 자세한 내용은 [OLE DB 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)을 참조하세요.  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 
### <a name="report-models"></a>보고서 모델  

 Oracle 데이터베이스를 기반으로 모델을 만들 수도 있습니다.  
::: moniker-end
   
### <a name="platform-and-version-information"></a>플랫폼 및 버전 정보  

 플랫폼 및 버전 지원에 대한 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  

  
## <a name="see-also"></a>참고 항목

 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
