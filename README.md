# Sitecore 9.0 in Docker

Docker images for Sitecore 9, a XM1 CM and a SQL Server. The Sitecore Install Framework (SIF) is used to install Sitecore inside the CM image following the official installation guidance. Windows 10 1709 (Fall Creators Update) is needed since it has support for the new smaller windowsservercore versions (7GB vs 13GB).

## Preparations

1. Download [Packages for XM Scaled](https://dev.sitecore.net/~/media/617694E165634C1E92BD30D894C24AA9.ashx) and unzip.
1. Copy **Sitecore 9.0.0 rev. 171002 (OnPrem)_cm.scwdp.zip** into **.\sitecore-xm1\install**.
1. Unzip **XM1 Configuration files rev.171002.zip** and copy **sitecore-XM1-cm.json** into **.\sitecore-xm1\install**.
1. Copy your **license.xml** into into **.\sitecore-xm1\install**.
1. Open **Sitecore 9.0.0 rev. 171002 (OnPrem)_cm.scwdp.zip** and the following files into **.\sitecore-sql\install**:
   1. Sitecore.Core.dacpac
   1. Sitecore.Master.dadcpac
   1. Sitecore.Web.dacpac
   1. Sitecore.ExperienceForms.dacpac
1. Build with: `docker-compose build` (takes a while).

## Usage

1. Start: `docker-compose up`
1. Get IP: `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' sitecoreninedocker_sitecore_1` and open with browser.

## Persistence

If you need persistence you can manually build the Sitecore image specifying an external SQL server:

    docker image build --build-arg SQL_SERVER=XXX --build-arg SQL_USER=XXX --build-arg SQL_PASSWORD=XXX --build-arg SQL_DB_PREFIX=XXX ./sitecore-xm1

Or you can roll your own Dockerfile using this as a base and add your own ConnectionStrings.config.