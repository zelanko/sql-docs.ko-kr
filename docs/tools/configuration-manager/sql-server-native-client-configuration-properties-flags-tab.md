---
title: SQL Server Native Client 구성 속성(플래그 탭)
description: SQL Server Native Client 구성 속성 대화 상자의 플래그 탭에 있는 옵션에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: bd8d00c4db1a327ca46ffcae1761faf5af85d32a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481514"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 구성 속성(플래그 탭)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  이 머신의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 라이브러리 파일에서 제공하는 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버와 통신합니다. 이 페이지에서는 이전에 SSL(Secure Sockets Layer)이라고 알려진 TLS(전송 계층 보안)를 사용하여 암호화된 연결을 요청하도록 클라이언트 컴퓨터를 구성합니다. 암호화된 연결을 설정할 수 없으면 연결되지 않습니다.  
  
 로그인 프로세스는 항상 암호화됩니다. 아래 옵션은 데이터 암호화에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통신을 암호화하는 방법과 서버 인증서의 루트 인증 기관을 신뢰하도록 클라이언트를 구성하는 방법은 “[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 암호화” 및 “방법: [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 암호화 연결 사용([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager)"을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 참조하세요.  
  
## <a name="options"></a>옵션  
 **프로토콜 암호화 강제 사용**  
 TLS를 사용하여 연결을 요청합니다.  
  
 **서버 인증서 신뢰**  
 **아니요** 로 설정하면 클라이언트 프로세스에서 서버 인증서의 유효성을 검사합니다. 클라이언트와 서버는 각각 공인 인증 기관에서 발급한 인증서를 가지고 있어야 합니다. 클라이언트 컴퓨터에 인증서가 없거나 인증서 유효성 검사에 실패하면 연결이 종료됩니다.  
  
 **예** 로 설정하면 클라이언트가 서버 인증서의 유효성을 검사하지 않으므로 자체 서명된 인증서를 사용할 수 있습니다.  
  
 **서버 인증서 신뢰** 는 **프로토콜 암호화 강제 사용** 이 **예** 로 설정된 경우에만 사용할 수 있습니다.  
  
  
