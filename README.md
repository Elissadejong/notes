# notes
from sklearn.preprocessing import StandardScaler
import pickle

# Pickle - you'll use it at least for these steps:
# to save the scaler
# to save the encoder
# to save the model

transformer = StandardScaler()
transformer.fit(X_train_num)

# saving in a pickle
with open('std_transformer.pickle', 'wb') as file:
    pickle.dump(transformer, file)
    
# loading from a pickle  
with open('std_transformer.pickle', 'rb') as file:
    loaded_transformer = pickle.load(file)

X_train_ = loaded_transformer.transform(X_train_num)
X_test_ = loaded_transformer.transform(X_test_num)

# if you need to un-scale afterwards, speacially if you scaled target variable:
unscaled_X_train = loaded_transformer.inverse_transform(X_train_)

# it makes sense to scale the target variable as well
unscaled_X_train[0][0]

# API WRAPPER
def get_all_song_ids_from_artists(artists_ids, show = True):
    final_track_ids = []
    for artist in artists_ids:
        album_ids = get_album_ids_from_artist(artist)
        track_ids = get_track_ids_from_albums(album_ids)
        final_track_ids.append(track_ids)
        if show:
            print(sp.artist(artist)["name"], ":", len(track_ids))
    return [i for j in final_track_ids for i in j]
