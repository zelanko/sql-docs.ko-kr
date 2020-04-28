---
title: 데이터 품질 클라이언트 애플리케이션 실행
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: da099b6a3aca31dd0acdc82f7e2bdbdf13c7c24e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75244125"
---
# <a name="run-the-data-quality-client-application"></a>데이터 품질 클라이언트 애플리케이션 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]을(를) 실행하고 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에 로그온합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 DQSInstaller.exe 파일을 실행하여 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 설치를 완료해야 합니다. 자세한 내용은 [DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 DQS_MAIN 데이터베이스에 대해 세 가지 DQS 역할(dqs_adminstrator, dqs_kb_editor 또는 dqs_kb_operator) 중 하나가 있어야 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에 로그온할 수 있습니다.  
  
##  <a name="run-data-quality-client"></a><a name="Run"></a>Data Quality Client 실행  
 설치된 컴퓨터에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 를 실행하려면 다음과 같이 진행합니다.  
  
1.  **시작**을 클릭하고 **모든 프로그램**을 가리킨 다음 **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, **Data Quality Services**, **Data Quality 클라이언트**를 차례로 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서  
  
    1.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 애플리케이션을 연결할 서버를 지정합니다. **(로컬)** 을 선택하여 로컬 컴퓨터의 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에 연결할 수 있습니다. 아래쪽 화살표를 클릭 하 고 다른 서버에 ** \<대>한 네트워크 찾아보기** 를 선택 하 여 다른 서버에 연결 하거나 이름으로 로컬 서버에 연결할 수도 있습니다. **서버 찾아보기** 대화 상자가 표시됩니다. **로컬 서버** 탭이나 **네트워크 서버** 탭에서 서버를 선택할 수 있습니다.  
  
    2.  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 와 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]사이의 데이터 전송을 암호화하려면 **옵션**을 클릭하고 **연결 암호화** 확인란을 선택합니다.  
  
3.  **연결**을 클릭합니다.  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면이 나타납니다. 자세한 내용은 [데이터 품질 클라이언트 홈 화면](../data-quality-services/data-quality-client-home-screen.md)을 참조하세요.  
  
  
