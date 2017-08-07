>[!NOTE]
>リソースを作成すると、以降は定期的に、可用性グループの構成に基づいて可用性グループの `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` の値を Pacemaker リソース エージェントが自動的に設定します。 たとえば、可用性グループに 3 つの同期レプリカがある場合、エージェントは `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` を `1` に設定します。 詳細およびその他の構成オプションについては、「[High availability and data protection for availability group configurations](..\linux\sql-server-linux-availability-group-ha.md)」 (可用性グループ構成の高可用性とデータ保護) を参照してください。 