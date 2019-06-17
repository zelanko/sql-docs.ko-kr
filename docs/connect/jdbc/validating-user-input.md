---
title: 사용자 입력 유효성 검사 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 35a357edee6293f40663628fd0cb66817d042b97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798523"
---
# <a name="validating-user-input"></a>사용자 입력 유효성 검사

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

데이터에 액세스하는 응용 프로그램을 만드는 경우 모든 사용자 입력은 입증되기 전까지 악의적일 수 있다고 가정해야 합니다. 그렇지 않으면 응용 프로그램이 쉽게 공격 당할 수 있습니다. 발생할 수 있는 공격 유형 중 하나가 SQL 삽입입니다. 이 공격에서는 구문 분석 및 실행을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 나중에 전달되는 문자열에 악성 코드가 추가됩니다. 이러한 공격 유형을 피하기 위해 가능한 한 매개 변수와 함께 저장 프로시저를 사용해야 하고 항상 사용자 입력의 유효성을 검사해야 합니다.

서버로의 반복 이동으로 인한 시간을 절약할 수 있으므로 클라이언트 코드에서 사용자 입력의 유효성 검사는 중요합니다. 또한 유효하지 않고 클라이언트측 유효성을 무시하는 입력을 catch하기 위해 서버의 저장 프로시저에 대한 매개 변수의 유효성 검사도 중요합니다.

SQL 삽입 및 방지 방법에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "SQL 삽입"을 참조하세요. 저장 프로시저 매개 변수의 유효성 검사에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "저장 프로시저([!INCLUDE[ssDE](../../includes/ssde_md.md)])"를 참조하세요.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)
