---
title: SQL Server Data Tools 설치 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.package.stub
ms.assetid: 6f8616cb-9119-42c3-a9b1-936e088763e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a847748b0f0025402da1feb794f5c441ea2a3f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773571"
---
# <a name="install-sql-server-data-tools"></a>SQL Server Data Tools 설치
이 항목에서는 SQL Server Data Tools 설치 방법을 설명합니다. SQL Server Data Tools 다운로드 페이지([최신 SQL Server Data Tools 설치](http://go.microsoft.com/fwlink/?LinkID=616714))에서 SQL Server Data Tools로 업데이트할 수 있습니다.  
  
Visual Studio 2012를 사용하든 Visual Studio 2013을 사용하든 간에 최신 기능을 사용하려면 최신 SQL Server Data Tools 업데이트를 설치합니다.  
  
## <a name="sql-server-data-tools-for-visual-studio-2013"></a>Visual Studio 2013용 SQL Server Data Tools  
SQL Server Data Tools는 Visual Studio 2013 Express for Web, Visual Studio 2013 Express for Desktop, Visual Studio Community 2013 및 Professional SKU를 비롯한 모든 유료 SKU에서 제공됩니다. Visual Studio 2013을 설치한 후 도구 -> 확장 및 업데이트 -> 업데이트로 이동하여 설치할 업데이트가 있는지 알아볼 수 있습니다.  
  
## <a name="sql-server-data-tools-for-visual-studio-2012"></a>Visual Studio 2012용 SQL Server Data Tools  
SQL Server Data Tools는 Visual Studio 2012의 전문 SKU 이상에서 제공됩니다. Visual Studio 2012 및 2012년 11월 버전 이상, SQL Server Data Tools 업데이트를 설치한 후에는 SQL Server Data Tools에서 설치할 업데이트가 있는 경우 이에 대한 메시지가 표시됩니다. 자세한 내용은 [업데이트 확인 대화 상자](../ssdt/check-for-updates-dialog-box.md)를 참조하세요.  
  
Visual Studio 2012가 설치되어 있지 않으면 SQL Server Data Tools에서는 Visual Studio 2012 통합 셸을 설치하고 SQL Server Data Tools를 설치합니다.  
  
## <a name="administrative-installation-point"></a>관리 설치 지점  
여러 컴퓨터 또는 인터넷 액세스가 없는 컴퓨터에 SQL Server Data Tools를 설치해야 할 경우 네트워크 공유 또는 실제 매체에 관리 설치 레이아웃을 만들고 해당 설치 지점으로부터 설치를 수행할 수 있습니다.  
  
설치 레이아웃을 만들려면 SSDTSetup.EXE를 다운로드하고 `/layout`*location* 옵션을 사용해서 실행하여 *location*에 레이아웃을 만듭니다. 그런 후 사용자가 *location*에서 SSDTSetup.Exe를 실행할 수 있습니다.  
  
[최신 SQL Server Data Tools 설치](http://go.microsoft.com/fwlink/?LinkID=616714)로 이동해서 SSDTSetup.exe를 다운로드하고 Visual Studio 버전에 대한 링크를 클릭한 다음 해당 언어에 대한 SSDTSetup.exe를 다운로드합니다.  
  
