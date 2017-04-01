---
title: "Azure에서 R Server 전용 SQL Server 2016 Enterprise VM에 프로비전 | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Azure에서 R Server 전용 SQL Server 2016 Enterprise VM에 프로비전

Azure에서 R Server 전용 SQL Server 2016 Enterprise 가상 컴퓨터는 R 솔루션 지원을 위해 서버 환경을 빠르고 쉽게 구성할 수 있는 새로운 옵션입니다. 이 Azure 가상 컴퓨터는 Microsoft R Server(독립 실행형)로 미리 구성되었습니다. 

이 새 가상 컴퓨터는 이전에 Azure Marketplace에서 사용할 수 있었던 Windows 가상 컴퓨터용 RRE를 대체합니다. 

이 가상 컴퓨터에는 R 분석 내부 응용 프로그램 및 백엔드 시스템 배포를 위한 DeployR Enterprise도 포함되어 있습니다. 자세한 내용은 [About Deploy R](https://msdn.microsoft.com/microsoft-r/deployr-about)(배포 R 정보)을 참조하세요.


## R Server 가상 컴퓨터 프로비전

Azure VM을 처음 사용하는 경우라면 이 문서에서 포털을 사용하고 가상 컴퓨터를 구성하는 방법에 대해 자세히 확인하는 것이 좋습니다.
[가상 컴퓨터-시작](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

Microsoft Azure Marketplace에서 R Server VM을 만들려면 
1. **가상 컴퓨터**를 클릭하고 검색 상자에 *R Server*를 입력합니다.
2. **R Server Only SQL Server 2016 Enterprise**(R Server 전용 SQL Server 2016 Enterprise)를 선택합니다.
3. [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 문서에 설명된 대로 가상 컴퓨터를 계속 프로비전합니다. 
7. VM을 만들고 실행한 후에는 **연결** 단추를 클릭하여 연결 상자를 열어 새 컴퓨터에 로그인합니다.
8. 연결할 때 기본적으로 **서버 관리자**가 열리지만 추가 서버 구성은 필요하지 않습니다. 바탕 화면으로 이동하려면 **서버 관리자**를 닫고 다음 단계를 진행합니다.
    + 추가 R 도구 또는 개발 도구 설치
    + DeployR 구성  

Azure 클래식 포털에서 R Server VM을 찾으려면
1. **가상 컴퓨터**를 클릭한 후 **새로 만들기**를 클릭합니다.
2. **새로 만들기** 창에서 **계산** 및 **가상 컴퓨터**가 선택되어 있어야 합니다. 
3. **갤러리에서**를 클릭하고 VM 이미지를 찾습니다. 검색 상자에 *R Server*를 입력하거나 **Microsoft**를 클릭하여 **R Server Only SQL Server 2016 Enterprise**가 나타날 때까지 아래로 스크롤해도 됩니다.


## R 도구 설치
기본적으로 Microsoft R Server에는 RTerm 및 RGui 등 기본 R 설치를 통해 설치된 모든 R 도구가 포함됩니다. R를 사용하여 지금 바로 시작하려는 경우 RGui 바로 가기가 바탕 화면에 추가되어 있습니다.

그러나 RStudio, Visual Studio용 R 도구 또는 Microsoft R Client와 같이 추가 R 도구를 설치할 수도 있습니다. 다운로드 위치 및 지침은 다음 링크를 참조하세요.
+ [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [Windows용 RStudio](https://www.rstudio.com/products/rstudio/download/)

이러한 도구를 설치한 후에는 도구가 R Server 라이브러리를 가리키도록 해야 합니다.

## 가상 컴퓨터에서 DeployR 사용

이 VM에 설치되어 있는 DeployR 인스턴스를 사용하려면 몇 가지 추가 단계가 필요합니다. 

DeployR 인스턴스를 구성하려면

1. VM에서 **DeployR 관리자 유틸리티**를 엽니다.
2. [Post Installation Steps](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows)(사후 설치 단계)에서 설명한 대로 DeployR 관리자 암호를 설정합니다.
3. DeployR 웹 컨텍스트를 설정합니다. 자세한 내용은 [DeployR Admin Installation in the Cloud](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud)(클라우드에서 DeployR 관리자 설치)를 참조하세요. 
4. [Configuring Azure Endpoints](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints)(Azure 끝점 구성)에서 설명한 대로 VM에서 적절한 포트를 엽니다. 
4. [Updating the firewall](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall)(방화벽 업데이트)에서 설명한 대로 Windows 방화벽을 업데이트합니다. 

## Azure Storage 계정에서 데이터 액세스 

Azure Storage 계정에서 데이터를 사용해야 할 때 데이터에 액세스하거나 데이터를 이동하는 데 필요한 몇 가지 옵션이 있습니다.


+ [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)와 같은 유틸리티를 사용하여 저장소 계정에서 로컬 파일 시스템으로 데이터를 복사합니다. 

+ 저장소 계정에서 파일 공유에 파일을 추가하고 VM에 파일 공유를 네트워크 드라이브로 탑재합니다.  자세한 내용은 [Mounting Azure files](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)(Azure 파일 탑재)를 참조하세요. 

## ADLS(Azure Data Lake Storage) 계정에서 데이터 사용

WebHDFS를 사용하여 HDFS 파일 시스템에서와 동일한 방법으로 저장소 계정을 참조하는 경우 ScaleR을 사용하여 ADLS 저장소에서 데이터를 읽을 수 있습니다.  자세한 내용은 이 [설치 가이드](http://go.microsoft.com/fwlink/?LinkId=723452)를 참조하세요.

## 리소스

MSDSN 라이브러리 [R Server and Scale R](https://msdn.microsoft.com/microsoft-r)(R Server 및 Scale R)에서 Microsoft R에 대한 추가 설명서를 찾을 수 있습니다.  


일반적으로 R에 대해 알아보려면 다음 추가 리소스를 참조하세요. 
+ [DataCamp](http://www.datacamp.com) R에 대한 무료 소개 및 중간 과정을 제공하며, Revolution R을 사용하는 빅 데이터 작업에 대한 과정도 제공합니다.
+ [Stack Overflow](http://www.stackoverflow.com)(스택 오버플로) R 프로그래밍 및 ML 도구와 관련된 질문에 대한 좋은 리소스입니다. 
+ [Cross Validated](https://stats.stackexchange.com/)(교차 검증) 기계 학습에서 통계 문제에 대한 질문을 모아 놓은 사이트입니다.
+ [R Help mailing list archives](https://www.r-project.org/mail.html)(R 도움말 메일 그룹 보관 ) 기록 정보에 유용한 리소스입니다. 
+ [MRAN 웹 사이트](https://mran.microsoft.com/documents/getting-started/) 다양한 R 리소스입니다.  

## 관련 항목:
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)
