# Download-ASTER-DEM-in-gee-editor and save in drive
var roi = Table users/kiranbhusalgeo/gandakiprovince
//import aster from gee dataset
var aster = ee.Image("NASA/ASTER_GED/AG100_003")

var elevation = aster.select('elevation')
var data = elevation.clip(roi)

Map.centerObject(roi,12)
Map.addLayer(data)

Export.image.toDrive({ 
  image: data,
  description: 'DEM_from_aster',
  folder : 'DTM report',
  scale: 10, 
  maxPixels: 1e13, 
  region: roi 
});
