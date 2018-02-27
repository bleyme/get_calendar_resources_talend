# Mining Google Calendar resources with Talend
Goal of this repo is to parse all resources in Google Calendar G Suite application and extract all events. From those events create an interactive graph showing resource usage from your company.

# Table of contents

  * [Requirements](#requirements)
  * [Installation](#installation)
     * [Create Google Cloud project](#create-google-cloud-project)
     * [Define GoogleContexts.csv location](#define-googlecontexts.csv-location)
     * [Configure GoogleContexts.csv](#configure-googlecontexts.csv)
     * [Configure MySQL table](#configure-mysql-table)
  * [Basic Overview](#basic-overview)
  * [Usage](#usage)

# Requirements

 - [Talend Open Studio for MDM](https://fr.talend.com/products/mdm/mdm-open-studio/)
 - [Google Cloud Platform](https://console.cloud.google.com/)
 - [GetGoogleToken](#) (already imported in this repo)
 - Admin account on G Suite domain

# Installation
## Create Google Cloud project
Create a Google Project at this url: https://console.cloud.google.com/
Then go to APIs & Services > Credentials and create an OAuth Client ID of type "Other":
![enter image description here](https://lh3.googleusercontent.com/HWRDRWaRjIx92RWhojm1GYSQAe37j4jAAVg76oBBzSi4egv0YRjpZZsvODva0cA5k4rA9bGfHs3bXlmwII_t71BjgspxMqAb9q0L0qApwkKkVFFaUTpchCjkov6ct2RzOQHj5GUJY-KdpGpQ1WR2W0MOuSKpUsEkaxtWZOOtCky8fkGUS5V9CQLM-NyugHw_POa5Ir_4e6xueJWR9YSDR0DrioOtcyUf8Sj7UC_8pA6saoPfBiI-L4SVwPh_G7VcswXvZSi1rrKQxKtYIUU39QSm10wsN-reeE0gEU4gLMljWUCrGZGWoiOggseO9ICqAkuqT3q4ZAb1rPHjjKuDTKWBXm5Hdhc187ec7Hm3kA3sJHlZMl0sWuam2ktnUlIFXMoRCL8I-PtA2OGIRSsTGQSQXAnb-GAnjFkFu0MCqOhGtW0-n2RSAlZyIJ3IFrWaXXr7rPu6RrOxpT3ODtDGYdkD8xfEvcgDpf3N9uWkq_wZXNcfs2FK089ST9EsbIHh32W-b2XokSuHQzFb-8KK0nosv7mhl-JmG38qF2S8iE4hwhCunLxLz8WTa0qkuOTs5Us8CJFFFb8z3WaFk03qOMNrVs9OpnBaQjV7keOm=w382-h285-no)

![enter image description here](https://lh3.googleusercontent.com/nzI5ZYZeXHN4Ow1w94SS-l3Ue3zywrfXxPBvi0Y70X12wEPHmwTkgxEjXHCB0xXpwpfAmFnY7guVUQsSRgxb3wJjIemVvSsCWqiyBbDalyjjwC34Oy46ubJKbEkzUJId8OjEDmIY_yhItER2Wg8srAcpq6VgiQhJVvlWIJnmQK5DYTQvWzauQr0Zw6rm9Oz-JDTnRLONIYqMkf5IyqXS3b-Ra5IWs1Os-IYZX2rD0VXulQwOYPP6h4IsJsHnVeCT0uuZMG-diAy6iZrLlpplk0USqF6yLdVaeb9ukbDFgw9LcOATOuR_w2yGyHvYi-Ip4cr_FOzR8X-DC0UKxyq3TtegT-9iCSMjRM33vXpF7I13FtQhoFNZ98rnsyISqF4rMFQGot-U2szG7eyHTB0hx8M_OgqwG94IKIhMmVrdJq0K-LvhVVbj8QOo84j18QhLgbqtduthJlH2KlO80HHmdzu5xI51V5nwvC_HiDk9Bs_OgYCEtuLZj4oBDyugLDP87QKqSH0nw36OPaxBn4LulbuXiYg17cgz8K3Mh9zhxfVg7589aQlUmPNfs_6pICGteQmx0eeFO2eBeIUsono6NftQgYwTPBod1788Wi0Z=w470-h233-no)

From here Cloud Console will provide you the following :
 - Client ID
 - Client Secret

Go to APIs & Services > Library:
![enter image description here](https://lh3.googleusercontent.com/ku3IQhpwe9KySbsB_CO2a9C96M3TMoSOCn0n5wuhez6QU8Q4L8bLLTkgk3lnAXE1ydAckE6kp-amywr0mV832zIrvsMnsJOdI-L483atXFphXU46PGvfGmZL7yzgNTTHpRgF46oca8YPm42FYsAT1fXDKLczLBGxQiSgax-LJETIwxn0uxBl_lXR6ybcZOZdSvAaC6egz7Q5TWmYP52N4rtW79Y-TYliEekVaCjrWeQfDFw37wWGXMNgOUxD30yDfXr7g6RsgPcD_R-ujnwfXJJrp_7LvYBKZ4NbHCTCPC7b9hwl5eWx8DVqZYs04tUmyOnAxzRYt_MfDGFGkb-MTv5vb05eaC4Q_e2hMQd88lmJ5LJ4YgcYnF_zddcCp2gWd7bopS4diEeYKDiEiLUmZ6zMWOOjWskdhecmj3gIYEljVgC-idBwZWe3G-B44nn1mHLVUUQvM2VON4h4jGbxm6D6-qCA9svICSMIOe1Yw8pW_WyKsN5o0XO_tRCAz_oFzDhf_ZcSiSQtA6-oI4-MzxS78o4vL8lm19hEjSekFFlMm5ETSdn2Yib1d9fYj2XoMQIsVuvaeXDwIKjsCRqsr6KW2ETBkqiNAKyqVcfL=w479-h217-no)
Search for **Google Calendar** and **Admin SDK** and enable.

## Define GoogleContexts.csv location
Here we need to specify in Talend job where will be located your data and GoogleContexts.

Edit Talend job and in context tab, specify the location of GoogleContexts.csv in path context:
![enter image description here](https://lh3.googleusercontent.com/QBcfO-Z-nJrjpNWNya8AQLxZh1Sax1qj3Bgov4pJl8Ieihpgs4NRTmb9lR4Nlf1xZ8fm8S_vq78ozy6SQ19Q_WF3QL6_upN1hNb4tw1McwzNDq70SYpXzM_yUAeGdpDWcImWhYDMyj5OlVx8AqPtrQY_488veAuDb-BMwFVeuL_FLukfwXI9IVqqSxh3PdVaK5YZKMifJyVOixpOPz-Mo19gXo2hsx7HztA86rSNPJZWvAYKHCkzuRa5fiOXE0eS_uwcxv7JKxbzsPLqW3Fcxc6GjDHvzhhHdKSLKSJGoVehUTvVidCNa4HGdFbDtbje0B9rMphvuwf17Q3TX5uNZEwUEXZnAFcYriNL3heNcfbl4pmJKv4qzaVi7pqnWoGlCOT1w7QNm7S-k0piLF0_0Mpk55Uvhw50PcTCcryzZk_n59-qotZXinn5h1pYjMB7nH7FTZNxJGHPUGZTIaMa60DV4UCdtjB-3DjLhun3oAHVCw5pHHQGbvamn6xsnKA50l0GRTOSza_tJvZmYyjaIDESb1yF6IZp4NWgBdBtQzNTCpdDc5gJNsVoK2pPuiIaz6uuFJHISRt-tFvG9J9she0AdRlLtDdVIuYNQxsn=w1290-h252-no)

In this example the location of GoogleContexts.csv file is located in the following folder: D:/Softs/talend-mdm-studio-6.5.1/workspace/TALEND/data/

## Configure GoogleContexts.csv
Once Google cloud project created and API enabled, create a file GoogleContexts.csv (or download it from this repo) in location specified in [Define GoogleContexts.csv location](#define-googlecontexts.csv-location). 

Fill it with the right credentials:

    client_id;YOUR_CLIENT_ID
    client_secret;YOUR_SECRET_ID
    scope;https://www.googleapis.com/auth/calendar https://www.googleapis.com/auth/admin.directory.resource.calendar.readonly
    customer_id;YOUR_CUSTOMER_ID

Replace **YOUR_CLIENT_ID** and **YOUR_SECRET_ID** that you had on [Create Google Cloud project](#create-google-cloud-project) section.

Replace **YOUR_CUSTOMER_ID** with your unique Customer ID that you can find here: [admin.google.com](https://admin.google.com) > Security > Set up single sign-on (SSO).

Customer ID is visible in SSO URL, here in bold: https://accounts.google.com/o/saml2/idp?idpid=**CUSTOMER_ID_HERE**

Scopes required required for the job are the following:
 - https://www.googleapis.com/auth/calendar
 - https://www.googleapis.com/auth/admin.directory.resource.calendar.readonly



## Configure MySQL table
Create table CHECK_CALENDAR with the below request:

    CREATE TABLE `CHECK_CALENDAR` (
      `resourceId` varchar(300) NOT NULL,
      `resourceName` varchar(100) DEFAULT NULL,
      `buildingId` varchar(100) DEFAULT NULL,
      `resourceEmail` varchar(100) DEFAULT NULL,
      `resourceCategory` varchar(100) DEFAULT NULL,
      `id` varchar(300) NOT NULL,
      `email` varchar(100) DEFAULT NULL,
      `startdate` datetime DEFAULT NULL,
      `enddate` datetime DEFAULT NULL,
      `summary` varchar(300) DEFAULT NULL,
      `status` varchar(45) DEFAULT NULL,
      PRIMARY KEY (`id`,`resourceId`)
    ) ENGINE=InnoDB DEFAULT CHARSET=latin1;
    
On Talend, there is a tMysqlOutput component component waiting for your credentials:
![enter image description here](https://lh3.googleusercontent.com/WX4Arx4q9CkOq2hDj5bqzs9mbJhUihd210k8wsNa4HT_7KZgtc2jFg-6rstl80a2tHCiKu558zg4ZA0kFfVeQK_Vtxh11m_XcKx2DnHP_rvRQh1paPqu0yXCym0hjGKZJ4RFewLW6IosJ65PuWrDsfY5hMcYzzAKpPynefygNwLkuVcvX2cRqguNX7sxNRlZDRyaEwIegJo0SS8gGY1_iw9Cur7d4gr9hgmlYpP1mNwAOv1rHs6554FubRNugPdsY3aNxMAx6lGC8tu73jk_T2wADjBBCiPiTX95BBLloLsHbXr4WThsDhLhl4fuRvhrJfwXgDsvJKXz7WieIHtY2jFoAfXsWKyoHmZwr6nUPD_nw9TU2A-Wu3zqz-wW597K-DRuMm_GNC5ipY4qeNFfdbp1-yoo6E5N0ZzEZpWay8AjIsjpSD3DNq26pK3tHILzxamqNs3UN5tKw0fsjeyWfC9aeT6LflRXDTBf0pw3FT1PRvtlmz2m86ghYpvk0nCj4g85krXOfFS5UpLZWteT6ql6yBwMnMCudjmunqUvptsJJPvTINWSCUzec7nHHT8kPbbxV2p7qNkFVzbt7ur_WPZCxDTflzyCmKjep8le=w854-h253-no)
Component is located here:
![enter image description here](https://lh3.googleusercontent.com/no5okPomOPLWCi4TnY8RiMQkY38cE_uiDXXMll77MuYOJLPpXXhIUqHXEDghpjUAC-sAuuaGTHHs23fBy11pvULnbZ5xGmbop7G3ouRKIJn1VXDc-PU4I1iOCh0j2VSb_hmZMCJdHB-1r0nUodx-8Zdm0yjxtp9aD30doRS8RWg1rP1m_VNWg-LniQGDJp8x4GpESzxGC5uP_T22tUyN5VErtrTnTMw_ZKYRSn33FbwNrqRK8Dp-QSOKKWwIo5iWIoxTeQlEOMpVZ1z5-4VAhI8lQ3XAYyDSbdm8zuqmBGFc21r5qUH-XpvsrnS7WL74oHHvrvwF9_jy8UAWkhWScvtYR8D1CD4Kpyfy_sGHllqAFrUuwlddY3FbQOD3V92LdM7IW0NCCuzhWmf-tne1XGnoxIxRX-u4yKqdzcIHR0avTvNzPBvNSQsQ1yk-wpRzWJbRxFwhDO0yg-wqLPpn0f1RgJE1LwZHUWxM9o5nhTtFJXdkQpXikNkc9QeiGt70KR9hF1JFkQuV2FUdZVM9CPxHfcs5X7qN6BwDKxCKJYB0md7Gb8paOAZD3Ofu0YUMtMVRcWOlF_RfOIvPCS5Y48IGVO07y_z_Rvc6kcio=w840-h312-no)

# Basic Overview

![enter image description here](https://lh3.googleusercontent.com/kkljB4zljuWvXXO059ylRHs54nLrWh0A78_IdgYkTUGrn4tM5wACRxvJqGIXBaoHsjJt2yXG6U8ml1tCmZLgGr0vY_3-AdTFcGtPx7_TGioDi98dGS6zQMSPm-ReRxncF-B3WYPFqR2IvqErxyShzf9qO8IQ5ybq9gQ9rgy4kc8_QypC275Zuq10xNDmplwROhlbObvfRGxpiPtcDB0ZkrnsZwMG6EOluE6EpcjFvcCkw4QySCcQvEIBpcEO6m1AyZdK1RTAbfau3b_f2kjOgJWvsZd9L1zLjmRumqErhBmWT9AGoHHo88OSnmzk9VXm23lg9hpHg6FTQaWNpyFewhOnGf7pQ1m7vZoljUaXwfkrpTmlW_8whYNQbs3mDmE0KqN4Fi19zgjPhC4Elb6fL6ipt_peD8uIaYaQLNR_OmMgMRINwDjEvpHhwBt3cVGle7Tnuvr_Ym8gf7dEoa5r_mnoCl55owwHLdfWWymj0QiJBDZA9x_eEFIchLFMujUDJgMwSimx2xwQrQ_dZUg4yqXMCOW1TDN34p0thQNdO0IeTvoiK8gshJE3C82NtkZvD_e2FWjjyv2O7WznjeiJQos_oAuLCyGi5SBnCpkg=w1424-h772-no)

tRunjob is the first executed component and is running our main job called **getGoogle_tokens** and then make sure GoogleContexts.csv is updated.

When executed, this job will first get an access token thanks to getGoogletokens job.
Once done, it will fetch the following API endpoint to retrieve all resources from your domain: 
`https://www.googleapis.com/admin/directory/v1/customer/"+context.customer_id+"/resources/calendars`

Then it will parse the content of resources.json with a loop to process each resources.
For each resources it will get all events and get resources metadata to build unique csv file for each resource containing the following data:

| Data source | Field |
|--|--|
| Resource | resourceId |
| Resource | resourceName |
| Resource | buildingId |
| Resource | resourceEmail |
| Resource | resourceCategory |
| Event | id |
| Event | email |
| Event | startdate |
| Event | enddate |
| Event | summary |
| Event | status |

For each of those, it will be imported in a MySQL database. Choice of this one is because it's mostly well supported by a lot of BI tools. 
You can also import all csv files created in any BI tool as well.

# Usage 

## Job execution
When executed the first time, access_token is not yet retrieved. Therefore you have to authorize your application requesting Gmail:
You will receive for the first time a message saying the following:

    [statistics] connecting to socket on port 3721
    [statistics] connected
    Refresh token and access token not found.
    https://accounts.google.com/o/oauth2/auth?scope=https://www.googleapis.com/auth/calendar https://www.googleapis.com/auth/admin.directory.resource.calendar.readonly&state=123456789qwertyui&redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=code&client_id=366972809643-356921stug411n6jvgohstq0gdhkufvc.apps.googleusercontent.com&approval_prompt=auto&include_granted_scopes=true&access_type=offline

URL has been generated according to your client id and scopes you defined. The process is the following:
 - Copy paste URL on a browser and get authorization 
 - Copy paste authorization code and put in Talend in message box :
![enter image description here](https://lh3.googleusercontent.com/Qk3B8Da3L_zdRDUbH428G60627iY-cFAwp_g5h308aTLeu37K0BTQa5jBjSZIAeQIUXX4byfelEhH6OBREcwgd7xZzmLLCNlCW3esYk_r3TUViuBVpNMVrNSpJfulNDxkI0GGt9JAobZ9xJPz1vQJDtl7S4Fq3Ion6y4vueBZG4-rbhprr85TaLB0c_DRhkSaeSoJTVFkhGb7WxNyj42ZFZROTKQ3q744g0M1Zg51tjOHyIOqkWeKw5ah5X4pmoOWeAMJ5UZEPSX_sNUkTDfHMvltrTza1UDk0K310ZJZHPjjqtG9VYSJ9ke066qvXaeniV-SGTD8VveoNo8FJ3Rr5cYej_HNFwtAbEX_Zg3nptYmeWppdKtWU2DlEILb_CeY2YQKNBNGysSURJLNC2PPHBgsZYvTMFeOSoUv9Dh1Axf2jfYAScEwJqE2svqXisJvcysOePAkjbC_ajflBgmJvTSw--CbYOFPK4hAajlQfG4uvQKVgwlg-IlzsEy3SVpFN5bMcjGUBgZ2YcfPCeQrKJMORLH1c7RKRFFMjxSFZZaQcbqiaVr-7miNIknR2ggoh2E8dtGpZSyz9dSVkRJSTVrbjiU8DPvZzg6obII=w526-h120-no)

When clicked on Ok, access_token is generated. This step must be done only the first time.

Executing this job will download all resources and events in location you defined in [Configure GoogleContexts.csv location](#configure-googlecontexts.csv-location) in subfolder called **events**

It will automatically import in MySQL table all events from all resources

## Requesting for free/busy in resources
Once imported on MySQL, we can request all events and group it by days and resources. Like this we have a full overview on resource usage for every days :

    SELECT date(startdate),
    resourceName,
    buildingId,
    TIME_TO_SEC(SEC_TO_TIME(SUM(UNIX_TIMESTAMP(enddate) - UNIX_TIMESTAMP(startdate))))/60 as 'BOOKED_MIN',
    TIME_TO_SEC(SEC_TO_TIME(28800))/60 - (TIME_TO_SEC(SEC_TO_TIME(SUM(UNIX_TIMESTAMP(enddate) - UNIX_TIMESTAMP(startdate))))/60) as 'FREE_MIN',
    TIME_TO_SEC(SEC_TO_TIME(28800))/60 as 'TOTAL_MIN'
    
    FROM CHECK_CALENDAR
    WHERE startdate <= CURDATE()
    
    GROUP BY YEAR(startdate), MONTH(startdate), DAY(startdate), resourceName
    ORDER BY YEAR(startdate) DESC, MONTH(startdate) DESC, DAY(startdate) DESC

From here you can import contents in any BI tool managing MYSQL such as Tableau or Data Studio and get easy result of your Calendar Resources usage. 

Example once imported on Data Studio:

**Example time consumed on resource A**
Time consuming from 2009 to 2018
![enter image description here](https://lh3.googleusercontent.com/3x-K8t5lQYwesA2sSu-7hiyNJ_IjVnbTCeDxaaxEejQrWHY5idWevl6d1bNnMSDVbwJ6E72IJI7fuKVmaJohylwuAiLsxcc0YdmKVbjBuzUA-fWR8ry07c6GcRLZ9ZCakdEEmzc7KfDbV6aLsh1BAnhqU29sSHK6wd9pH3QuwNkzp7f_FhSL7kscR9mDHFQAhcdd1j0sSjwWPm6c_nK2jsFxsgy0LMi8xqYidCcFgR5mVET5JSdUzCVVXNmH5TzQTU3SQ21dNwGKSdqK5JIT0OJ-gXMkLkao7QDG0NwgqnqEQaq7Zz01ud6rf1_LQFd8nnB5tJ7M05y_ltfUS9HqWSHQULJRtCn0G8ooAF_2fl5LGBsQmJlO51OZuhD5g14cqQZEhfVuHFlFy_Zn44wVEhQ9ldI0REM45vgupY2gMq5QbamahiAT_KCjB49mVsvzWUfqgVXsJ1SbQ0UjpDDbQxn_ahyRGP97QbzE92tilHHUDbJGxB4nE1n7sEZKCtxZqdEkjfb1LtoO7JGW5h4d83DoWurS2FJPxjgMNvrXcvWhPFRNZiuhJ8Ifp2KGlpt5O_wNhEqXgnXk1uzi30UyGrPYYImAFEnWYW-ZLMC2=w1338-h533-no)

**Example time consumed on resource B**
Time consuming from 2009 to 2018
![enter image description here](https://lh3.googleusercontent.com/0bVjHtpMua039VvIbbw0hY4F08poQ6HFtbxAXp16hvAm6ZUkwdju00XFUV2jzNPkVKOnnFTRRF76a1mww9hQE7VXF5yhNXFchvSGM7Zup1eeK2YftPt8Dy6uqPvgCKBB-Xi7M4FKsMJvtp7yri7T36U33E7arx1dMmRH__57Cl-TdmY7YqP6nKdSosX55zvsRsxtl-wfd_9ujfYaP9u6kYDvfMCuJkOCkqLB5_pKDiELPm7tbR1n2v02Oi-o6qUxTzx0L4trUddyFOkB9mhD5WFwmrTow_IPLku_483DgUlOp9IthWwBqVATE-RaKyTRcXPyz0SvJ5-jyD6ylFyOEzEQy8PKp1yE_g9tTRdgfksJ_VVZWAlc9GKkZn9K2kFijiuP0dn8CuSyDblajYp6OW_8Mf143aFxXCf9pyygaK62uap0OXahTvPVOrE6BjbASG-w7uI4IXDQj5h4hpo5gXjM9UQZtKM9OphZ70YUn3uACsv5OWA5WO_wwdITwoOIW1YYXTOzqonIIededvLQ750tj495yqKHEY2JRVXNg7S2zlIASdtFDG7ztlrk0G-AyEwWr5p-a5-MZtPxnuV4Qk4Cs8H_qdLmEMAE4Uvk=w1355-h554-no)

This way you are able to know if a resource such as a meeting room is very used or not.