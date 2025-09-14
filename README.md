];

export default function App() {
  useEffect(() => {
    const loadAd = async () => {
      try {
        await AdMobInterstitial.setAdUnitID("ca-app-pub-3940256099942544/1033173712");
        await AdMobInterstitial.requestAdAsync({ servePersonalizedAds: true });
        await AdMobInterstitial.showAdAsync();
      } catch (error) { console.log("Interstitial Ad Error:", error); }
    };
    loadAd();
  }, []);

  const openLink = (url) => {
    Linking.openURL(url).catch(() => Alert.alert("Error", "Cannot open link"));
  };

  const renderPrayer = ({ item }) => (
    <View style={{ padding: 12, marginVertical: 6, backgroundColor: "#fff", borderRadius: 8 }}>
      <Text style={{ fontSize: 18, fontWeight: "600" }}>{item.title}</Text>
      <Text style={{ marginTop: 6 }}>{item.body}</Text>
    </View>
  );

  return (
    <SafeAreaView style={{ flex: 1, padding: 16, backgroundColor: "#f2f2f2" }}>
      <Text style={{ fontSize: 22, fontWeight: "700", marginBottom: 12 }}>Prayers & God’s Word</Text>
      <FlatList data={SEED_PRAYERS} keyExtractor={(item) => item.id} renderItem={renderPrayer} />
      <View style={{ marginTop: 20 }}>
        <AdMobBanner bannerSize="smartBannerPortrait" adUnitID="ca-app-pub-3940256099942544/6300978111" servePersonalizedAds onDidFailToReceiveAdWithError={(err) => console.log(err)} />
      </View>
      <View style={{ marginTop: 20 }}>
        <Button title="Visit Facebook Page" onPress={() => openLink(FACEBOOK_PAGE)} />
      </View>
      <View style={{ marginTop: 10 }}>
        <Button title="Offers / Support" onPress={() => openLink(SUPPORT_LINK)} />
      </View>
    </SafeAreaView>
  );
}' > App.js
