# -*- coding: utf-8 -*-
# this file is released under public domain and you can use without limitations

#########################################################################
## This is a sample controller
## - index is the default action of any application
## - user is required for authentication and authorization
## - download is for downloading files uploaded in the db (does streaming)
#########################################################################

from gluon.tools import Crud
crud = Crud(db)

#def index():
#    images = db().select(db.image.ALL, orderby=db.image.title)
#    #return dict(images=images)
#    return locals()
def index():
    listings = db().select(db.forSaleList.ALL, orderby = db.forSaleList.Title)
    #image = db.forSaleList(request.args(0,cast=int)) or redirect(URL('index'))
    return locals()
def showList():
    depts = db().select(db.forSaleList.ALL, orderby=db.forSaleList.Title)
    return locals()

@auth.requires_login()
def addItem():
    form = crud.create(db.forSaleList,next='showList')
    return locals()

@auth.requires_login()
def manageItems():
    grid = SQLFORM.grid(db.forSaleList)
    return locals()

#def show():
#    image = db.image(request.args(0,cast=int)) or redirect(URL('index'))
#    db.post.image_id.default = image.id
#    form = SQLFORM(db.post)
#    if form.process().accepted:
#        response.flash = 'your comment is posted'
#    comments = db(db.post.image_id==image.id).select()
    #return dict(image=image, comments=comments, form=form)
#    return locals()

def show():
    image = db.forSaleList(request.args(0,cast=int)) or redirect(URL('index'))
    return locals()



def user():
    """
    exposes:
    http://..../[app]/default/user/login
    http://..../[app]/default/user/logout
    http://..../[app]/default/user/register
    http://..../[app]/default/user/profile
    http://..../[app]/default/user/retrieve_password
    http://..../[app]/default/user/change_password
    http://..../[app]/default/user/bulk_register
    use @auth.requires_login()
        @auth.requires_membership('group name')
        @auth.requires_permission('read','table name',record_id)
    to decorate functions that need access control
    also notice there is http://..../[app]/appadmin/manage/auth to allow administrator to manage users
    """
    return dict(form=auth())


@cache.action()
def download():
    """
    allows downloading of uploaded files
    http://..../[app]/default/download/[filename]
    """
    return response.download(request, db)


def call():
    """
    exposes services. for example:
    http://..../[app]/default/call/jsonrpc
    decorate with @services.jsonrpc the functions to expose
    supports xml, json, xmlrpc, jsonrpc, amfrpc, rss, csv
    """
    return service()
