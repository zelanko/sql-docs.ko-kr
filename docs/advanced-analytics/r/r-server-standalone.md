---
title: "R Server(독립 실행형) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 3f0c567463c25a54829a988516890bead171f5ec
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="r-server-standalone"></a>R Server (Standalone)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft SQL Server 2016에서 릴리스 **R Server (독립 실행형)**, 엔터프라이즈 수준의 분석을 지원 하기 위한 해당 플랫폼의 일부로 합니다.  Microsoft R Server는 R 언어에 대 한 확장성 및 보안을 제공 하 고 오픈 소스 오른쪽의 메모리 내 한계를 해결 SQL Server R 서비스와 같은 Microsoft R Server (독립 실행형)는 데이터의 병렬 및 청크 처리에 R 사용자가 메모리에 들어갈 수 있는 것 보다 훨씬 더 큰 데이터를 사용할 수 있도록 제공 합니다.

SQL Server 2017에 학습, 컴퓨터 커뮤니티의 한 폭넓은 지원을 이용할 수와 텍스트 분석 워크 로드와 심층 학습에 대 한 인기 있는 라이브러리를 포함 하는 Python 언어에 대 한 지원이 추가 되었습니다.  이 광범위 한 집합이 언어를 반영 하도록 했습니다도 이름을 변경 하려면 **Microsoft 컴퓨터 학습 Server (독립 실행형)**합니다.

## <a name="benefits-of-microsoft-r-server"></a>Microsoft R Server의 이점

여러 플랫폼에서 분산 컴퓨팅용 Microsoft R Server를 사용할 수 있습니다. SQL Server 설치 프로그램에서 설치할 때 게시 및 배포 모델에 대 한 Windows 기반 서버 및 필요한 도구를 모두 가져옵니다. 다른 플랫폼에 대 한 자세한 내용은 MSDN 라이브러리의 다음이 리소스를 참조 합니다.

+ [Introducing Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)(Microsoft R Server 소개)
+ [R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)(Windows용 R Server)

RevoScaleR 라이브러리 및 SQL Server에 배포할 수 있는 R 솔루션을 만드는 데 필요한 도구를 가져오는 데 개발 클라이언트로 사용할 Microsoft R Server를 설치할 수 있습니다.

## <a name="whats-new-in-microsoft-machine-learning-server"></a>Microsoft, 학습 서버 컴퓨터의에서 새로운 기능

SQL Server 2017 설치 프로그램을 사용 하 여 컴퓨터 학습 서비스 (독립 실행형) 설치 하는 경우 이제 Python 언어를 추가 하려면 옵션이 제공 됩니다. 당연히 R 언어 여전히 옵션을 지원된 하며 필요한 경우에 두 언어를 설치할 수 있습니다.
 
서버 설치에 SQL Server 2017 CTP 2.0 mrsdeploy 패키지 및 작업 활용 모델에 사용 되는 다른 유틸리티도 있습니다. 자세한 내용은 참조 [mrsdeploy 해결해줍니다](../../advanced-analytics/operationalization-with-mrsdeploy.md)합니다.

SQL Server 기계 학습의 Enterprise 사용자 바인딩 이라는 프로세스에서의 R 구성 요소를 업그레이드 하려면 Microsoft R Server에 대 한 다운로드 가능한 설치 관리자를 사용할 수 있습니다. 자세한 내용은 참조 [업그레이드 및 SQL Server 인스턴스를 사용 하 여 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>Microsoft R Server 또는 학습 Server 컴퓨터 (독립 실행형)를 가져옵니다.

 Microsoft R Server를 설치 하기 위한 여러 가지가 있습니다.

+ SQL Server 설치 마법사를 사용 하 여

  [독립 실행형 R 서버 만들기](../r/create-a-standalone-r-server.md)

  SQL Server 2016 설치 프로그램을 실행 **Microsoft R Server (독립 실행형)**합니다. R 언어는 기본적으로 추가 됩니다.
  SQL Server 2017 설치 프로그램을 실행 또는 **학습 Server 컴퓨터 (독립 실행형)** R, Python, 또는 둘 다 선택 합니다.

  > [!IMPORTANT]
  > 에 서버를 설치 하는 옵션은는 **공유 기능** 설치 합니다. 다른 모든 구성 요소를 설치 하지 마십시오.
  >
  > 가급적 서버는 SQL Server R Services 또는 SQL Server 컴퓨터 학습 서비스 설치 되어 있는 컴퓨터에 설치 하지 마십시오.

+ SQL Server 설치 프로그램에 대 한 명령줄 옵션을 사용 합니다.

  [명령줄에서 Microsoft R Server 설치](../r/install-microsoft-r-server-from-the-command-line.md)

  SQL Server 설치 프로그램은 다양 한 명령줄 인수를 통해 무인된 설치를 지원합니다.

+ 독립 실행형 설치 관리자를 사용 하 여

  [Windows 용 Microsoft R Server를 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)합니다.

  이제 Microsoft R Server 또는 Microsoft 학습 서버 컴퓨터의 새 인스턴스를 설정 하는 새로운 Windows installer를 사용할 수 있습니다.  Microsoft R Server (및 Microsoft 컴퓨터 학습 서버)를 사용 하려면 SQL Server Enterprise 계약이 필요 합니다. 그러나 독립 실행형 설치 관리자를 실행 한 후 기존 설치에 대 한 지원 정책 업데이트 됩니다 새로운 최신 수명 주기 정책을 사용 하 여. 이 지원 옵션을 사용 하면 컴퓨터 학습 구성 요소에 대 한 업데이트 예상 되는 SQL Server 서비스 릴리스를 사용 하는 경우 보다 더 자주 적용 됩니다.

  
+ SQL Server 인스턴스 업그레이드

  [R Services의 인스턴스를 업그레이드 하려면 SqlBindR를 사용 하 여](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.
  
  독립 실행형 설치 관리자를 사용 하 여은 R입니다. 최신 버전을 사용 하도록 SQL Server 2016 R Services의 인스턴스를 업그레이드 하려면 설치 관리자를 실행 하는 경우 최신 수명 주기 지원 정책 서버에 적용 됩니다 하 고 R 구성 요소를 더 자주 업데이트 받습니다.
  
  > [! 참고 (를) 현재이 업데이트 메서드는 SQL Server 2016의 기존 설치에만 사용할 수 있습니다. 그러나 업그레이드 지원이 제공 됩니다 SQL Server 2017 나중에 있습니다.

## <a name="related-machine-learning-products"></a>관련된 시스템 제품 학습

+ R 서버와 azure 가상 컴퓨터

  [R 서버 가상 컴퓨터 프로 비전](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure 마켓플레이스 R Server를 포함 하는 여러 가상 컴퓨터 이미지를 포함 합니다. Microsoft Azure에서 새 R Server 가상 컴퓨터를 만들 서버를 개발 하 고 예측 모델을 배포에 사용 하도록 설정 하는 가장 빠른 방법은 합니다. 이미지 크기 조정 및 이미 구성 된 공유에 대 한 R 응용 프로그램 분석을 포함 하 고 백 엔드 시스템과 R 통합을 쉽게 기능 함께 제공 됩니다.

+ 데이터 과학 가상 컴퓨터

  [데이터 과학 가상 컴퓨터-Windows 2016 미리 보기](http://aka.ms/dsvm/win2016)

  R 서버, SQL Server를 포함 하는 데이터 과학 가상 컴퓨터의 최신 버전 및 가장 인기 있는 도구에 대 한 기계 학습의 배열을 모든 사전 설치 하 고 테스트입니다. Jupyter 노트북, 만들고, Julia에서 솔루션을 개발 MXNet, CNTK, 및 TensorFlow과 같은 심층 학습 GPU 사용이 가능한 라이브러리를 사용 합니다.

## <a name="resources"></a>리소스

샘플, 자습서 및 Microsoft R Server에 대 한 자세한 내용은 참조 [Microsoft R 제품](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)합니다.

## <a name="see-also"></a>관련 항목:

 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)

