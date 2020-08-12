---
title: SSDT(SQL Server Data Tools)의 이전 릴리스
description: 어느 버전의 SSDT 및 SSDT-BI가 어느 버전의 Visual Studio와 함께 작동하는지 알아봅니다. 다양한 버전의 SSDT 및 SSDT-BI를 설치하는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 06/17/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: f6fea0264cdbd28c8f6665f5f0d67eda4a8da3c9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009945"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>SQL Server Data Tools(SSDT 및 SSDT-BI)의 이전 릴리스

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SSDT(SQL Server Data Tools)는 관계형 데이터베이스, Analysis Services 모델, Reporting Services 보고서, Integration Services 패키지 등의 SQL Server 콘텐츠 형식을 빌드하기 위한 프로젝트 템플릿 및 디자인 화면을 제공합니다.

SSDT는 이전 버전과 호환되므로 항상 [최신 SSDT](download-sql-server-data-tools-ssdt.md)를 사용하여 이전 버전의 SQL Server에서 실행되는 데이터베이스, 모델, 보고서 및 패키지를 설계하고 배포할 수 있습니다.

기존에 SQL Server 콘텐츠 형식을 만드는 데 사용하는 Visual Studio 셸은 **SQL Server Data Tools**, **SQL Server Data Tools - Business Intelligence**, **Business Intelligence Development Studio**등과 같은 다양한 이름으로 출시되었습니다. 이전 버전에는 고유한 프로젝트 템플릿 집합이 함께 제공되었습니다. 하나의 SSDT에서 모든 프로젝트를 함께 이용하려면 [최신 버전](download-sql-server-data-tools-ssdt.md)이 있어야 합니다. 그러지 않으면 여러 이전 버전을 설치하여 SQL Server에서 사용되는 모든 템플릿을 가져와야 합니다. Visual Studio 버전당 셸이 하나만 설치되지만, 두 번째 SSDT를 설치하기만 하면 누락된 템플릿이 추가됩니다.

## <a name="previous-ssdt-releases"></a>이전 SSDT 릴리스

관련 섹션에서 다운로드 링크를 선택하여 이전 SSDT 버전을 다운로드합니다.

| SSDT 버전 | Visual Studio 버전 |
|--------------|-----------------------|
| [15.8](#ssdt-for-visual-studio-vs-2017) | 2017 |
| [17.4](#ssdt-for-visual-studio-vs-2015) | 2015 |
| [16.5](#ssdt-for-visual-studio-vs-2013) | 2013 |
| [11.1.50727.1](#ssdt-for-visual-studio-vs-2012) | 2012 |

### <a name="ssdt-for-visual-studio-vs-2017"></a>VS(Visual Studio) 2017용 SSDT

**[Visual Studio 2017용 SSDT(15.8) 다운로드](https://go.microsoft.com/fwlink/?linkid=2124319)**

이 **Visual Studio 2017용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40a)

### <a name="ssdt-for-visual-studio-vs-2015"></a>VS(Visual Studio) 2015용 SSDT

이 버전의 SSDT를 설치하려면 ISO 이미지를 다운로드해야 합니다. ISO 파일은 SSDT에 필요한 모든 구성 요소가 들어 있는 자체 포함된 파일이고 다시 시작 가능한 다운로드 관리자를 사용하여 다운로드할 수 있어 네트워크 대역폭이 제한되어 있거나 덜 안정적인 상황에 유용합니다. 다운로드되면 ISO를 드라이브로 탑재할 수 있습니다.

설치 단계:

1. **[Visual Studio 2015용 SSDT(17.4)를 다운로드](https://go.microsoft.com/fwlink/?linkid=2132817)** 합니다.

2. ISO 이미지를 엽니다.

3. *SSDTSetup.exe* 파일을 실행합니다.

    ![ISO 이미지](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

이 **Visual Studio 2015용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.

| 언어 | SHA256 해시 |
|----------|-------------|
| [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [프랑스어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [독일어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [일본어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [한국어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [러시아어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [스페인어](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2013"></a>VS(Visual Studio) 2013용 SSDT

이 버전의 SSDT를 설치하려면 ISO 이미지를 다운로드해야 합니다. ISO 파일은 SSDT에 필요한 모든 구성 요소가 들어 있는 자체 포함된 파일이고 다시 시작 가능한 다운로드 관리자를 사용하여 다운로드할 수 있어 네트워크 대역폭이 제한되어 있거나 덜 안정적인 상황에 유용합니다. 다운로드되면 ISO를 드라이브로 탑재할 수 있습니다.

설치 단계:

1. **[Visual Studio 2013용 SSDT(16.5)를 다운로드](https://go.microsoft.com/fwlink/?linkid=832312)** 합니다.

2. ISO 이미지를 엽니다.

3. *SSDTSetup.exe* 파일을 실행합니다.

    ![ISO 이미지](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

이 **Visual Studio 2013용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.

| 언어 | SHA256 해시 |
|----------|-------------|
| [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [프랑스어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [독일어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [일본어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [한국어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [러시아어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [스페인어](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2012"></a>VS(Visual Studio) 2012용 SSDT

이 버전의 SSDT를 설치하려면 ISO 이미지를 다운로드해야 합니다. ISO 파일은 SSDT에 필요한 모든 구성 요소가 들어 있는 자체 포함된 파일이고 다시 시작 가능한 다운로드 관리자를 사용하여 다운로드할 수 있어 네트워크 대역폭이 제한되어 있거나 덜 안정적인 상황에 유용합니다. 다운로드되면 ISO를 드라이브로 탑재할 수 있습니다.

설치 단계:

1. **[Visual Studio 2012용 SSDT(11.1.50727.1)를 다운로드](https://go.microsoft.com/fwlink/?linkid=518814)** 합니다.

2. ISO 이미지를 엽니다.

3. *SSDTSetup.exe* 파일을 실행합니다.

    ![ISO 이미지](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

이 **Visual Studio 2012용 SSDT** 릴리스는 다음 언어로 설치할 수 있습니다.

| 언어 | SHA256 해시 |
|----------|-------------|
| [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x804) | 78F20325648CFF49D9C58A26186E0AC199D104B3CF634E5663B4B262BEC69C07 |
| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x404) | A2722380AF2EE1E8BB52B4FA54A61BAB411E5E5FD5B050108F81ED23DC87366D |
| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x409) | 748EF78D3F9CC6FE360432C378EA690DE51AEB2C747E87D43E08448D26F93A91 |
| [프랑스어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40c) | 40E6504169BF618EDC7EB5B62D1215DC96726D6EEC3CA8EC3EEB49044E4B6FB7 |
| [독일어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x407) | C45C974E6B8F9611BA2AC1EE90C5C507992BCE5693BF46F6C7C138591ED6A123 |
| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x410) | C1B20CDB41C7B1B5DE76A71F9A091A6FDF5186B12F6AA269DA6338B3CB2D91A6 |
| [일본어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x411) | BF56958B904C1C5F28084BD0B16928B6CBFEC83EB3F0C913EC364FA335241943 |
| [한국어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x412) | 9023B0656785C357A67E39EB76A2806B923C2BD17342D7226A8ADA384A9F4E28 |
| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x416) | ACAD9FE03729E289ECE821D92C56CFB1D7FCCEA8423ABF1E164BF3C67ABEFEFB |
| [러시아어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x419) | E2191D787BA833DF4A85B064C5373DC44099E76214FBF9505728702D4D6B83F0 |
| [스페인어](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40a) | 6D81FB572A7003C54C29D2ACF076D2CED4A1CA80F329BFF9D41A806920D64EEE |

> [!Note]
> SSDT는 두 가지 최신 버전의 Visual Studio를 지원합니다. Visual Studio 2019 릴리스부터 Visual Studio 2015 및 이전 버전용 SSDT 버전은 더 이상 업데이트되지 않습니다. Visual Studio 2010용 SSDT를 더 이상 사용할 수 없습니다. 자세한 내용은 [이 SSDT 팀 블로그 게시물](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/)의 *FAQ* 섹션을 참조하세요.

## <a name="sql-bi-analysis-services-reporting-services-integration-services"></a>SQL BI: Analysis Services, Reporting Services, Integration Services

BI 템플릿은 SSAS 모델, SSRS 보고서 및 SSIS 패키지를 만드는 데 사용됩니다. BI Designer는 특정 버전의 SQL Server에 연결되어 있습니다. 최신 BI 기능을 사용하려면 최신 버전이 있는 BI Designer를 설치하세요.

## <a name="bi-designers"></a>BI Designer

[Visual Studio 2013용 SSDT-BI 다운로드](https://www.microsoft.com/download/details.aspx?id=42313)(SQL Server 2014, SQL Server 2012, SQL Server 2008 및 2008 R2)

[Visual Studio 2012용 SSDT-BI 다운로드](https://www.microsoft.com/download/details.aspx?id=36843)(SQL Server 2014, SQL Server 2012, SQL Server 2008 및 2008 R2)

BIDS(Business Intelligence Development Studio)는 SQL Server 설치 프로그램을 통해 설치됩니다. 웹 다운로드(SQL Server 2008, 2008 R2)가 없습니다.

SQL Server 2012 또는 2014의 경우 **Visual Studio 2012용 SSDT-BI** 또는 **SSDT-BI f또는 Visual Studio 2013**등과 같은 다양한 이름으로 출시되었습니다. 두 버전은 Visual Studio 버전만 다릅니다.

## <a name="next-steps"></a>다음 단계

- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)
- [SSDT(SQL Server Data Tools) 릴리스 정보](release-notes-ssdt.md)
- [SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)
- [Azure Data Studio 다운로드](../azure-data-studio/download-azure-data-studio.md)
- [SQL 도구 및 유틸리티](../tools/overview-sql-tools.md)