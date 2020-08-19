---
description: 로그 파일 공간 사용 최소화
title: 로그 파일 공간 사용 최소화 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: rothja
ms.author: jroth
ms.openlocfilehash: 986d527f0d4f59053a53a8b566d28d43151c0f99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452165"
---
# <a name="minimizing-log-file-space-usage"></a>로그 파일 공간 사용 최소화
SQL Server 데이터베이스에 작업 볼륨이 많은 경우 로그 파일이 빠르게 채워질 수 있습니다 (따라서 서버가 중지 됨). **검사점에서 Truncate** 로그 파일을 설정 하 여 데이터베이스에 대 한 로그 파일의 수명을 현저 하 게 확장할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5에서 검사점에서 잘라내기를 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server Enterprise Manager를 시작 하 고 서버의 트리를 연 다음 데이터베이스 장치 트리를 엽니다.  
  
2.  이 기능을 사용할 데이터베이스의 이름을 두 번 클릭 합니다.  
  
3.  **데이터베이스** 탭에서 **Truncate**를 선택 합니다.  
  
4.  **옵션** 탭에서 **검사점에서 로그 자르기**를 선택 하 고 **확인**을 클릭 합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0에서 검사점에서 잘라내기를 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server Enterprise Manager를 시작 하 고 서버의 트리를 연 다음 데이터베이스 트리를 엽니다.  
  
2.  이 기능을 사용할 데이터베이스의 이름을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  
  
3.  **옵션** 탭에서 **검사점에서 로그 자르기**를 선택 하 고 **확인**을 클릭 합니다.  
  
 **검사점에서 자르기** 기능에 대 한 자세한 내용은 Microsoft SQL Server 설명서를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


