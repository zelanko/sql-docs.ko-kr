---
description: SQL Server에 연결 (AccessToSQL)
title: SQL Server에 연결 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ceb77a97-d6d5-4a92-90a6-342e97d12b54
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 06a305d705e404a2045525e584faddf6b9530cb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418599"
---
# <a name="connect-to-sql-server-accesstosql"></a>SQL Server에 연결 (AccessToSQL)
**SQL Server에 연결** 대화 상자를 사용 하 여 마이그레이션하려는 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. **SQL Server에 연결** 대화 상자에 액세스 하려면 **파일** 메뉴에서 **SQL Server에 연결**을 클릭 합니다.  
  
## <a name="options"></a>옵션  
**서버 이름**  
연결할 SQL Server 인스턴스를 입력 하거나 선택 합니다. 기본적으로 가장 최근에 연결한 인스턴스가 표시 됩니다.  
  
-   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 **localhost** 또는 점 (**.**)을 입력할 수 있습니다.  
  
-   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.  
  
-   다른 컴퓨터의 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름 (예: *MyServer*MyInstance)을 입력 합니다 \\ *MyInstance*.  
  
**서버 포트**  
인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 포트 (1433)에서 연결을 허용 하도록 구성 되지 않은 경우 포트 번호를 입력 합니다. 그렇지 않으면이 값을 비워 둡니다.  
  
**Database**  
개체 및 데이터를 마이그레이션할 데이터베이스를 지정 합니다. 에 다시 연결 하는 경우에는이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**인증**  
에 연결 하는 데 사용 되는 인증 방법을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 현재 Windows 계정을 사용 하려면 Windows 인증을 선택 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그인 및 암호를 지정 하려면 인증을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
**사용자 이름**  
인증을 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 인스턴스에 대 한 로그인을 입력 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Windows 인증을 사용 하는 경우에는이 옵션을 사용할 수 없습니다.  
  
**암호**  
인증을 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 인스턴스의 로그인에 대 한 암호를 입력 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Windows 인증을 사용 하는 경우에는이 옵션을 사용할 수 없습니다.  
  
**연결 암호화**  
SQL Server에 안전 하 게 연결 하려는 경우 **연결 암호화** 확인란을 선택 하 여 연결 암호화를 사용 합니다.  
  
**서버 인증서 신뢰**  
이 옵션을 사용 하려면 **서버 인증서 신뢰** 확인란을 선택 합니다.  
  
> [!NOTE]  
> **서버 인증서 신뢰**를 사용 하려면 "Encrypt"를 **True**로 설정 해야 합니다.  
  
