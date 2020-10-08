---
title: SqlClient의 데이터 검색 및 분류
description: SQL Server 데이터베이스에서 데이터 분류를 지원하는지 확인하는 방법 및 SqlDataReader 개체를 통해 데이터 분류 정보에 액세스하는 방법을 설명합니다.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b53e71c4c302145af14c1f2e37f30fe0e3c8f8e2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725724"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient의 데이터 검색 및 분류

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[데이터 검색 및 분류](../../../relational-databases/security/sql-data-discovery-and-classification.md?view=sql-server-2017)는 데이터베이스에서 중요한 데이터를 검색, 분류, 레이블 지정하기 위한 고급 서비스의 집합입니다. SqlClient는 기본 원본이 기능을 지원하는 경우 읽기 전용 데이터 검색 및 분류 정보를 노출하는 API를 제공합니다. 이 정보는 SqlDataReader를 통해 액세스합니다.

이 샘플 애플리케이션은 SqlDataReader의 데이터 분류 속성에 액세스하는 방법을 보여 줍니다.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**참고 항목**  

 [SQL Server 기능 및 ADO.NET](sql-server-features-adonet.md)