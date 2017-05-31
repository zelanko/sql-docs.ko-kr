---
title: "연결 속성 대화 상자 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8e258a6b81a9061c08ba4df098afa4e67c74df3a
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="connection-properties-dialog-box"></a>연결 속성 대화 상자
이 대화 상자를 사용하여 현재 연결 속성을 확인할 수 있습니다. 다양한 개체 탐색기 대화 상자에서 **연결 속성 보기** 를 클릭하면 이 대화 상자를 사용할 수 있습니다. 이 페이지에 표시된 속성은 읽기 전용입니다.  
  
**데이터베이스**와 같은 속성을 변경하려면 **연결 속성** 대화 상자를 열기 전에 개체 탐색기로 원하는 데이터베이스에 연결합니다.  
  
SQL Azure의 쿼리 제한 시간은 30분입니다.  
  
## <a name="authentication"></a>인증  
현재 연결에 대한 인증 속성을 표시합니다. 인증 속성은 연결을 설정할 때 사용한 로그인 및 인증 방법입니다. 인증 속성을 변경하려면 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 연결을 끊은 다음 원하는 연결 옵션을 사용하여 개체 탐색기를 서버에 다시 연결합니다.  
  
**인증 방법**  
현재 연결에 사용된 인증 방법입니다.  
  
**사용자 이름**  
연결 인증에 사용된 로그인의 사용자 이름입니다.  
  
## <a name="connection-category"></a>연결 범주  
현재 연결에 대한 연결 속성을 표시합니다. 대부분의 연결 속성은 연결하는 동안 **서버에 연결** 대화 상자의 **연결 속성** 탭에서 선택합니다.  
  
**데이터베이스**  
현재 연결된 데이터베이스의 이름입니다. 이름을 변경하려면 SQL 편집기 도구 모음을 사용합니다.  
  
**SPID**  
서버에서 연결에 할당한 시스템 프로세스 ID입니다. 이 연결에 대해서는 변경할 수 없습니다.  
  
**네트워크 프로토콜**  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 연결의 네트워크 프로토콜입니다. 이를 변경하려면 원하는 연결 속성으로 다시 연결합니다.  
  
**네트워크 패킷 크기**  
서버와 통신할 때 사용되는 패킷 크기입니다. 이를 변경하려면 원하는 연결 속성으로 다시 연결합니다.  
  
**연결 제한 시간**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 연결할 때 대기하는 시간(초)입니다. 이 시간이 지나면 사용자에게 연결 실패 오류가 반환됩니다. 이를 변경하려면 원하는 연결 속성으로 다시 연결합니다.  
  
**실행 제한 시간**  
서버에서 태스크 실행이 완료되기까지 대기하는 시간(초)입니다. 이를 변경하려면 원하는 연결 속성으로 다시 연결합니다.  
  
**암호화됨**  
현재 연결의 암호화 여부를 나타냅니다. 이를 변경하려면 원하는 연결 속성으로 다시 연결합니다.  
  
## <a name="product-category"></a>Product Category  
현재 연결에 대한 제품 속성을 표시합니다. 이러한 속성은 서버 제품, 버전, 인스턴스 이름 및 데이터 정렬에 대해 설명합니다. 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설치 과정에서 설정됩니다.  
  
**제품 이름**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 이름입니다.  
  
**제품 버전**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 버전입니다.  
  
**서버 이름**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 실행 중인 컴퓨터의 이름입니다.  
  
**인스턴스 이름**  
서버의 인스턴스 이름입니다. 기본 인스턴스는 비어 있습니다.  
  
**언어**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품의 언어 버전입니다.  
  
**데이터 정렬**  
서버의 데이터 정렬입니다.  
  
## <a name="server-environment-category"></a>서버 환경 범주  
현재 연결의 서버 하드웨어 및 운영 체제와 관련된 서버 환경 속성을 표시합니다. 이러한 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 구성할 수 없습니다.  
  
**컴퓨터 이름**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 실행 중인 서버 컴퓨터의 이름입니다.  
  
**플랫폼**  
서버의 운영 체제 이름, 제조업체 이름 및 CPU 제품군입니다.  
  
**운영 체제**  
서버에 설치되어 있는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 버전입니다.  
  
**프로세서**  
서버의 프로세서 수입니다.  
  
**운영 체제 메모리**  
서버의 실제 메모리 전체 크기(MB)입니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server Management Studio의 속성 페이지](../../ssms/property-pages-in-sql-server-management-studio.md)  
[서버에 연결&amp;#40;로그인 페이지&amp;#41; 데이터베이스 엔진](../../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  

