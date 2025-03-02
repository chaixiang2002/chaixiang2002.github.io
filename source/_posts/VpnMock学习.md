Vpn调用了哪些？

public synchronized ParcelFileDescriptor establish(VpnConfig config)

- config.dnsServers = mMock.regroupDnsServer(config.dnsServers)

private SortedSet<Integer> getAppsUids(List<String> packageNames, int userHandle)

- uids.add(id);uids.remove(id);
- return uids;

void addUserToRanges(@NonNull Set<UidRange> ranges, @UserIdInt int userHandle,

- List<Integer> bypass = mMock.getBypassVpnPackages();
- for (int uid : getAppsUids(allowedApplications, userHandle, bypass, false))