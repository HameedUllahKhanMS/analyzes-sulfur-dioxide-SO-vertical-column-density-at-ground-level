    imageVisParam = {"opacity":1,"bands":["SO2_column_number_density"],"min":0.00006055849956225256,"max":0.0002895033185479587,"palette":["040274","040281","0502a3","0502b8","0502ce","0502e6","0602ff","235cb1","307ef3","269db1","30c8e2","32d3ef","3be285","3ff38f","86e26f","3ae237","b5e22e","d6e21f","fff705","ffd611","ffb613","ff8b13","ff6e08","ff500d","ff0000","de0101","c21301","a71001","911003"]};
var data = ee.ImageCollection("COPERNICUS/S5P/OFFL/L3_SO2")
                .filterDate('2023-01-01','2023-12-01');
var SO2 = data.select('SO2_column_number_density');
var SO2faislabad = SO2.mean().clip(faislabad);
var Vis = {
  min: -0.4051,
  max: 0.2079,
  palette: [
    '040274', '040281', '0502a3', '0502b8', '0502ce', '0502e6',
    '0602ff', '235cb1', '307ef3', '269db1', '30c8e2', '32d3ef',
    '3be285', '3ff38f', '86e26f', '3ae237', 'b5e22e', 'd6e21f',
    'fff705', 'ffd611', 'ffb613', 'ff8b13', 'ff6e08', 'ff500d',
    'ff0000', 'de0101', 'c21301', 'a71001', '911003'
  ],
};

Map.addLayer(
  SO2faislabad, Vis,
  'SO2 vertical column density at ground level'
);
Export.image.toDrive({
  image: SO2faislabad,
  description: 'F2023',
  scale: 30,
  region: faislabad,
  fileFormat: 'GeoTIFF',
});
