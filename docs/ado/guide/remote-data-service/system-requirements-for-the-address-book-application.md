---
description: 주소록 애플리케이션에 대한 시스템 요구 사항
title: 주소록 응용 프로그램에 대 한 시스템 요구 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: rothja
ms.author: jroth
ms.openlocfilehash: 59913c457702e39b9009cd2a8a138b2dbc5f9032
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759903"
---
# <a name="system-requirements-for-the-address-book-application"></a>주소록 애플리케이션에 대한 시스템 요구 사항
주소록 샘플 응용 프로그램을 설정 하려면 다음 소프트웨어 및 데이터베이스 요구 사항을 충족 해야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
 이 웹 응용 프로그램을 실행 하기 위한 서버 컴퓨터 소프트웨어 요구 사항은 다음과 같습니다.  
  
-   Microsoft Windows NT® Server 4.0, 서비스 팩 3 이상 또는 Microsoft Windows® 2000 서버.  
  
-   Active Server 페이지가 있는 Microsoft 인터넷 정보 서비스 (IIS) 버전 3.0 이상  
  
 이 웹 응용 프로그램을 실행 하기 위한 클라이언트 컴퓨터 소프트웨어 요구 사항은 다음과 같습니다.  
  
-   Microsoft Internet Explorer 4.0 이상  
  
-   Microsoft Windows NT 4.0 워크스테이션 또는 서버, Windows 2000 또는 Microsoft Windows 98.  
  
## <a name="database-requirements"></a>데이터베이스 요구 사항  
 이 샘플을 사용 하려면 다음이 있어야 합니다.  
  
-   운영 Microsoft® SQL Server 버전 6.5 이상 데이터베이스 서버입니다.  
  
-   데이터베이스를 만들고 예제 데이터로 채울 수 있는 권한입니다.  
  
-   엔터프라이즈 관리자 또는 ISQL 유틸리티 (SQL Server 7.0에서 쿼리 분석기 라고 함)를 통해 채워진 데이터의 유효성을 검사 합니다.  
  
 권한이 없는 경우 데이터베이스 관리자가 시스템을 설정 하 고 데이터베이스에 대 한 액세스 권한을 부여 하거나 데이터베이스를 설정 해야 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [주소록 SQL 스크립트 실행](./running-the-address-book-sql-script.md)   
 [DataControl 개체 (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [주소록 예제 애플리케이션 실행](./running-the-address-book-sample-application.md)